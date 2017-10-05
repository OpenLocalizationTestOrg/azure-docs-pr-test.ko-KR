---
title: "Azure PowerShell 스크립트 샘플 - VM 네트워크 트래픽 필터링 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - 인바운드 및 아웃바운드 VM 네트워크 트래픽을 필터링합니다."
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: e871ba2f370157936c2aaabc804dc9f5aea6d7ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a><span data-ttu-id="a4bb2-103">인바운드 및 아웃바운드 VM 네트워크 트래픽 필터링</span><span class="sxs-lookup"><span data-stu-id="a4bb2-103">Filter inbound and outbound VM network traffic</span></span>

<span data-ttu-id="a4bb2-104">이 스크립트 샘플은 프런트 엔드 및 백 엔드 서브넷이 있는 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a4bb2-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="a4bb2-105">프런트 엔드 서브넷에 대한 인바운드 네트워크 트래픽은 HTTP 및 HTTPS로 제한되지만, 백 엔드 서브넷에서 인터넷으로의 아웃바운드 트래픽은 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a4bb2-105">Inbound network traffic to the front-end subnet is limited to HTTP, and HTTPS, while outbound traffic to the Internet from the back-end subnet is not permitted.</span></span> <span data-ttu-id="a4bb2-106">스크립트를 실행한 후에는 두 개의 NIC가 있는 하나의 가상 컴퓨터가 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4bb2-106">After running the script, you will have one virtual machine with two NICs.</span></span> <span data-ttu-id="a4bb2-107">각 NIC는 서로 다른 서브넷에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4bb2-107">Each NIC is connected to a different subnet.</span></span>

<span data-ttu-id="a4bb2-108">필요한 경우 [Azure PowerShell 가이드](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)에 있는 지침을 사용하여 Azure PowerShell을 설치한 다음, `Login-AzureRmAccount`를 실행하여 Azure에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="a4bb2-108">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="a4bb2-109">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="a4bb2-109">Sample script</span></span>


<span data-ttu-id="a4bb2-110">[!code-powershell[주](../../../powershell_scripts/virtual-network/filter-network-traffic/filter-network-traffic.ps1  "VM 네트워크 트래픽 필터링")]</span><span class="sxs-lookup"><span data-stu-id="a4bb2-110">[!code-powershell[main](../../../powershell_scripts/virtual-network/filter-network-traffic/filter-network-traffic.ps1  "Filter VM network traffic")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="a4bb2-111">배포 정리</span><span class="sxs-lookup"><span data-stu-id="a4bb2-111">Clean up deployment</span></span> 

<span data-ttu-id="a4bb2-112">다음 명령을 실행하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4bb2-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="a4bb2-113">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="a4bb2-113">Script explanation</span></span>

<span data-ttu-id="a4bb2-114">이 스크립트는 다음 명령을 사용하여 리소스 그룹, 가상 네트워크 및 네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a4bb2-114">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="a4bb2-115">표에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4bb2-115">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="a4bb2-116">명령</span><span class="sxs-lookup"><span data-stu-id="a4bb2-116">Command</span></span> | <span data-ttu-id="a4bb2-117">참고 사항</span><span class="sxs-lookup"><span data-stu-id="a4bb2-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a4bb2-118">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a4bb2-118">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="a4bb2-119">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a4bb2-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a4bb2-120">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="a4bb2-120">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="a4bb2-121">서브넷 구성 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a4bb2-121">Creates a subnet configuration object</span></span> |
| [<span data-ttu-id="a4bb2-122">새-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="a4bb2-122">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="a4bb2-123">Azure 가상 네트워크 및 프런트 엔드 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a4bb2-123">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="a4bb2-124">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="a4bb2-124">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="a4bb2-125">네트워크 보안 그룹에 할당될 보안 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a4bb2-125">Creates security rules to be assigned to a network security group.</span></span> |
| [<span data-ttu-id="a4bb2-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="a4bb2-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) |<span data-ttu-id="a4bb2-127">특정 포트를 특정 서브넷에 허용하거나 차단하는 NSG 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a4bb2-127">Creates NSG rules that allow or block specific ports to specific subnets.</span></span> |
| [<span data-ttu-id="a4bb2-128">Set-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="a4bb2-128">Set-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="a4bb2-129">NSG를 서브넷에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="a4bb2-129">Associates NSGs to subnets.</span></span> |
| [<span data-ttu-id="a4bb2-130">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="a4bb2-130">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="a4bb2-131">인터넷에서 VM에 액세스하기 위한 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a4bb2-131">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="a4bb2-132">새-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="a4bb2-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="a4bb2-133">가상 네트워크 인터페이스를 만들고 가상 네트워크의 프런트 엔드 및 백 엔드 서브넷에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="a4bb2-133">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="a4bb2-134">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="a4bb2-134">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="a4bb2-135">VM 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a4bb2-135">Creates a VM configuration.</span></span> <span data-ttu-id="a4bb2-136">이 구성은 VM 이름, 운영 체제 및 관리자 자격 증명 등의 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a4bb2-136">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="a4bb2-137">이 구성은 VM을 만드는 중에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4bb2-137">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="a4bb2-138">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="a4bb2-138">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="a4bb2-139">가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a4bb2-139">Create a virtual machine.</span></span> |
|[<span data-ttu-id="a4bb2-140">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a4bb2-140">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="a4bb2-141">리소스 그룹 및 포함된 모든 리소스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="a4bb2-141">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a4bb2-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a4bb2-142">Next steps</span></span>

<span data-ttu-id="a4bb2-143">Azure PowerShell에 대한 자세한 내용은 [Azure PowerShell 설명서](https://docs.microsoft.com/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a4bb2-143">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="a4bb2-144">추가 네트워킹 PowerShell 스크립트 샘플은 [Azure 네트워킹 개요 설명서](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4bb2-144">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>