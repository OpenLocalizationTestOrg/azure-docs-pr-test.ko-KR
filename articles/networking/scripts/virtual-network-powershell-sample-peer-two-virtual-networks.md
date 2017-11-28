---
title: "Azure PowerShell 스크립트 샘플 - 2개 가상 네트워크 피어링 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - 2개 가상 네트워크 피어링"
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
ms.openlocfilehash: 51c0b98727e148671cfd7ab2b31ffd1c705d8a4e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="peer-two-virtual-networks"></a><span data-ttu-id="b2599-103">2개 가상 네트워크 피어링</span><span class="sxs-lookup"><span data-stu-id="b2599-103">Peer two virtual networks</span></span>

<span data-ttu-id="b2599-104">이 스크립트는 Azure 네트워크를 통해 동일한 지역에서 두 가상 네트워크를 만들고 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b2599-104">This script creates and connects two virtual networks in the same region trhough the Azure network.</span></span> <span data-ttu-id="b2599-105">스크립트를 실행한 후에 두 개의 가상 네트워크 간 피어링을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b2599-105">After running the script, you will create a peering between two virtual networks.</span></span>

<span data-ttu-id="b2599-106">필요한 경우 [Azure PowerShell 가이드](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)에 있는 지침을 사용하여 Azure PowerShell을 설치한 다음, `Login-AzureRmAccount`를 실행하여 Azure에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b2599-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="b2599-107">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="b2599-107">Sample script</span></span>

<span data-ttu-id="b2599-108">[!code-azurepowershell[주](../../../powershell_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.ps1 "두 개 네트워크 피어링")]</span><span class="sxs-lookup"><span data-stu-id="b2599-108">[!code-azurepowershell[main](../../../powershell_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.ps1 "Peer two networks")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="b2599-109">배포 정리</span><span class="sxs-lookup"><span data-stu-id="b2599-109">Clean up deployment</span></span> 

<span data-ttu-id="b2599-110">다음 명령을 실행하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2599-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="b2599-111">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="b2599-111">Script explanation</span></span>

<span data-ttu-id="b2599-112">이 스크립트는 다음 명령을 사용하여 리소스 그룹, 가상 컴퓨터 및 모든 관련된 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b2599-112">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="b2599-113">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2599-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="b2599-114">명령</span><span class="sxs-lookup"><span data-stu-id="b2599-114">Command</span></span> | <span data-ttu-id="b2599-115">참고 사항</span><span class="sxs-lookup"><span data-stu-id="b2599-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b2599-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b2599-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="b2599-117">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b2599-117">Creates a resource group in which all resources are stored.</span></span> | 
| [<span data-ttu-id="b2599-118">새-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="b2599-118">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork)| <span data-ttu-id="b2599-119">Azure Virtual Network 및 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b2599-119">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="b2599-120">Add-AzureRmVirtualNetworkPeering</span><span class="sxs-lookup"><span data-stu-id="b2599-120">Add-AzureRmVirtualNetworkPeering</span></span>](/powershell/module/azurerm.network/add-azurermvirtualnetworkpeering) | <span data-ttu-id="b2599-121">두 가상 네트워크 간에 피어링을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b2599-121">Creates a peering between two virtual networks.</span></span>  |
| [<span data-ttu-id="b2599-122">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b2599-122">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="b2599-123">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="b2599-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b2599-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b2599-124">Next steps</span></span>

<span data-ttu-id="b2599-125">Azure PowerShell에 대한 자세한 내용은 [Azure PowerShell 설명서](https://docs.microsoft.com/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b2599-125">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="b2599-126">추가 네트워킹 PowerShell 스크립트 샘플은 [Azure 네트워킹 개요 설명서](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2599-126">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>