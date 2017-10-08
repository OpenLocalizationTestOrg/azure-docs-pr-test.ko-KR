---
title: "aaaAzure PowerShell 스크립트 예제 필터 VM 네트워크 트래픽 | Microsoft Docs"
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
ms.openlocfilehash: 39eae6a43a8dc7f9fc616ef3ec50f95443fd3547
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a><span data-ttu-id="c664f-103">인바운드 및 아웃바운드 VM 네트워크 트래픽 필터링</span><span class="sxs-lookup"><span data-stu-id="c664f-103">Filter inbound and outbound VM network traffic</span></span>

<span data-ttu-id="c664f-104">이 스크립트 샘플은 프런트 엔드 및 백 엔드 서브넷이 있는 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c664f-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="c664f-105">인바운드 네트워크 트래픽을 toohello 프런트 엔드 서브넷은 제한 된 tooHTTP 및 아웃 바운드 동안 HTTPS 트래픽 toohello hello 백 엔드 서브넷에서 인터넷을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c664f-105">Inbound network traffic toohello front-end subnet is limited tooHTTP, and HTTPS, while outbound traffic toohello Internet from hello back-end subnet is not permitted.</span></span> <span data-ttu-id="c664f-106">Hello 스크립트를 실행 한 후 두 개의 Nic 하나의 가상 컴퓨터를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c664f-106">After running hello script, you will have one virtual machine with two NICs.</span></span> <span data-ttu-id="c664f-107">각 NIC가 연결 된 tooa 다른 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="c664f-107">Each NIC is connected tooa different subnet.</span></span>

<span data-ttu-id="c664f-108">필요한 경우 설치 명령 hello를 사용 하 여 Azure PowerShell hello 있는 hello [Azure PowerShell 가이드](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), 한 다음 실행 `Login-AzureRmAccount` toocreate Azure와의 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c664f-108">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="c664f-109">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="c664f-109">Sample script</span></span>


[!code-powershell[main](../../../powershell_scripts/virtual-network/filter-network-traffic/filter-network-traffic.ps1  "Filter VM network traffic")]

## <a name="clean-up-deployment"></a><span data-ttu-id="c664f-110">배포 정리</span><span class="sxs-lookup"><span data-stu-id="c664f-110">Clean up deployment</span></span> 

<span data-ttu-id="c664f-111">Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c664f-111">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="c664f-112">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="c664f-112">Script explanation</span></span>

<span data-ttu-id="c664f-113">이 스크립트는 리소스 그룹, 가상 네트워크 및 네트워크 보안 그룹 명령 toocreate 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c664f-113">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="c664f-114">Hello 테이블 링크 toocommand 특정 설명서에서 각 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="c664f-114">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="c664f-115">명령</span><span class="sxs-lookup"><span data-stu-id="c664f-115">Command</span></span> | <span data-ttu-id="c664f-116">참고 사항</span><span class="sxs-lookup"><span data-stu-id="c664f-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c664f-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c664f-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="c664f-118">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c664f-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c664f-119">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="c664f-119">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="c664f-120">서브넷 구성 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c664f-120">Creates a subnet configuration object</span></span> |
| [<span data-ttu-id="c664f-121">새-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="c664f-121">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="c664f-122">Azure 가상 네트워크 및 프런트 엔드 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c664f-122">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="c664f-123">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="c664f-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="c664f-124">보안 규칙 toobe tooa 네트워크 보안 그룹 할당을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c664f-124">Creates security rules toobe assigned tooa network security group.</span></span> |
| [<span data-ttu-id="c664f-125">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="c664f-125">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) |<span data-ttu-id="c664f-126">NSG 규칙을 허용 하거나 차단할 toospecific 서브넷 특정 포트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c664f-126">Creates NSG rules that allow or block specific ports toospecific subnets.</span></span> |
| [<span data-ttu-id="c664f-127">Set-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="c664f-127">Set-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="c664f-128">Toosubnets Nsg를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c664f-128">Associates NSGs toosubnets.</span></span> |
| [<span data-ttu-id="c664f-129">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="c664f-129">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="c664f-130">Hello 인터넷에서에서 공용 IP 주소 tooaccess hello VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c664f-130">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="c664f-131">새-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="c664f-131">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="c664f-132">가상 네트워크 인터페이스를 만들고 toohello 가상 네트워크의 프런트 엔드 및 백 엔드 서브넷에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c664f-132">Creates virtual network interfaces and attaches them toohello virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="c664f-133">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="c664f-133">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="c664f-134">VM 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c664f-134">Creates a VM configuration.</span></span> <span data-ttu-id="c664f-135">이 구성은 VM 이름, 운영 체제 및 관리자 자격 증명 등의 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c664f-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="c664f-136">hello 구성은 VM 만드는 동안 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c664f-136">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="c664f-137">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="c664f-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="c664f-138">가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c664f-138">Create a virtual machine.</span></span> |
|[<span data-ttu-id="c664f-139">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c664f-139">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="c664f-140">리소스 그룹 및 포함된 모든 리소스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="c664f-140">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c664f-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c664f-141">Next steps</span></span>

<span data-ttu-id="c664f-142">Azure PowerShell hello에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](https://docs.microsoft.com/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="c664f-142">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="c664f-143">추가 네트워킹 PowerShell 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 네트워킹 개요 문서](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="c664f-143">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
