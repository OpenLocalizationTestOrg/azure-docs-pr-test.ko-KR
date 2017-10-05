---
title: "Azure PowerShell 스크립트 샘플 - 다중 계층 응용 프로그램용 네트워크 만들기 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - 다중 계층 응용 프로그램을 위한 가상 네트워크를 만듭니다."
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
ms.openlocfilehash: ab49e78ef17b093d2bbe4e3276a1ece3a4247f91
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a><span data-ttu-id="14d9b-103">다중 계층 응용 프로그램을 위한 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="14d9b-103">Create a network for multi-tier applications</span></span>

<span data-ttu-id="14d9b-104">이 스크립트 샘플은 프런트 엔드 및 백 엔드 서브넷이 있는 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="14d9b-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="14d9b-105">프런트 엔드 서브넷에 대한 트래픽은 HTTP 및 SSH로 제한되며, 백 엔드 서브넷에 대한 트래픽은 MySQL(3306 포트)로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="14d9b-105">Traffic to the front-end subnet is limited to HTTP and SSH, while traffic to the back-end subnet is limited to MySQL, port 3306.</span></span> <span data-ttu-id="14d9b-106">스크립트를 실행한 후에는 웹 서버와 MySQL 소프트웨어를 배포할 수 있는 두 개의 가상 컴퓨터가 각 서브넷에 하나씩 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="14d9b-106">After running the script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span></span>

<span data-ttu-id="14d9b-107">필요한 경우 [Azure PowerShell 가이드](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)에 있는 지침을 사용하여 Azure PowerShell을 설치한 다음, `Login-AzureRmAccount`를 실행하여 Azure에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="14d9b-107">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="14d9b-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="14d9b-108">Sample script</span></span>


<span data-ttu-id="14d9b-109">[!code-powershell[주](../../../powershell_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.ps1  "다중 계층 응용 프로그램용 가상 네트워크")]</span><span class="sxs-lookup"><span data-stu-id="14d9b-109">[!code-powershell[main](../../../powershell_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.ps1  "Virtual network for multi-tier application")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="14d9b-110">배포 정리</span><span class="sxs-lookup"><span data-stu-id="14d9b-110">Clean up deployment</span></span> 

<span data-ttu-id="14d9b-111">다음 명령을 실행하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14d9b-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="14d9b-112">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="14d9b-112">Script explanation</span></span>

<span data-ttu-id="14d9b-113">이 스크립트는 다음 명령을 사용하여 리소스 그룹, 가상 네트워크 및 네트워크 보안 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="14d9b-113">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="14d9b-114">표에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="14d9b-114">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="14d9b-115">명령</span><span class="sxs-lookup"><span data-stu-id="14d9b-115">Command</span></span> | <span data-ttu-id="14d9b-116">참고 사항</span><span class="sxs-lookup"><span data-stu-id="14d9b-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="14d9b-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="14d9b-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="14d9b-118">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="14d9b-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="14d9b-119">새-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="14d9b-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="14d9b-120">Azure 가상 네트워크 및 프런트 엔드 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="14d9b-120">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="14d9b-121">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="14d9b-121">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="14d9b-122">백 엔드 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="14d9b-122">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="14d9b-123">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="14d9b-123">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="14d9b-124">인터넷에서 VM에 액세스하기 위한 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="14d9b-124">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="14d9b-125">새-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="14d9b-125">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="14d9b-126">가상 네트워크 인터페이스를 만들고 가상 네트워크의 프런트 엔드 및 백 엔드 서브넷에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="14d9b-126">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="14d9b-127">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="14d9b-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="14d9b-128">프런트 엔드 및 백 엔드 서브넷과 연결되는 NSG(네트워크 보안 그룹)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="14d9b-128">Creates network security groups (NSG) that are associated to the front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="14d9b-129">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="14d9b-129">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) |<span data-ttu-id="14d9b-130">특정 포트를 특정 서브넷에 허용하거나 차단하는 NSG 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="14d9b-130">Creates NSG rules that allow or block specific ports to specific subnets.</span></span> |
| [<span data-ttu-id="14d9b-131">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="14d9b-131">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="14d9b-132">가상 컴퓨터를 만들고 각 VM에 NIC를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="14d9b-132">Creates virtual machines and attaches a NIC to each VM.</span></span> <span data-ttu-id="14d9b-133">또한 이 명령은 사용할 가상 컴퓨터 이미지와 관리 자격 증명을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="14d9b-133">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="14d9b-134">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="14d9b-134">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="14d9b-135">리소스 그룹 및 이 그룹에 속한 모든 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="14d9b-135">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="14d9b-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="14d9b-136">Next steps</span></span>

<span data-ttu-id="14d9b-137">Azure PowerShell에 대한 자세한 내용은 [Azure PowerShell 설명서](https://docs.microsoft.com/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="14d9b-137">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="14d9b-138">추가 네트워킹 PowerShell 스크립트 샘플은 [Azure 네트워킹 개요 설명서](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14d9b-138">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>