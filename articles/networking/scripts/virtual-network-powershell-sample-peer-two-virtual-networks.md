---
title: "PowerShell 스크립트 샘플-aaaAzure 피어 두 가상 네트워크 | Microsoft Docs"
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
ms.openlocfilehash: 8b66085c35de2fc30bcef57a00d7d370911d1f3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="peer-two-virtual-networks"></a><span data-ttu-id="b215d-103">2개 가상 네트워크 피어링</span><span class="sxs-lookup"><span data-stu-id="b215d-103">Peer two virtual networks</span></span>

<span data-ttu-id="b215d-104">이 스크립트를 만들고 hello에 두 개의 가상 네트워크를 연결 동일한 지역 trhough hello Azure 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="b215d-104">This script creates and connects two virtual networks in hello same region trhough hello Azure network.</span></span> <span data-ttu-id="b215d-105">Hello 스크립트를 실행 한 후 두 개의 가상 네트워크 간의 피어 링을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b215d-105">After running hello script, you will create a peering between two virtual networks.</span></span>

<span data-ttu-id="b215d-106">필요한 경우 설치 명령 hello를 사용 하 여 Azure PowerShell hello 있는 hello [Azure PowerShell 가이드](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), 한 다음 실행 `Login-AzureRmAccount` toocreate Azure와의 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b215d-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="b215d-107">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="b215d-107">Sample script</span></span>

[!code-azurepowershell[main](../../../powershell_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.ps1 "Peer two networks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="b215d-108">배포 정리</span><span class="sxs-lookup"><span data-stu-id="b215d-108">Clean up deployment</span></span> 

<span data-ttu-id="b215d-109">Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b215d-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="b215d-110">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="b215d-110">Script explanation</span></span>

<span data-ttu-id="b215d-111">이 스크립트 명령 toocreate 리소스 그룹에서 가상 컴퓨터를 다음 hello를 사용 하 고 모든 관련 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="b215d-111">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="b215d-112">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b215d-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b215d-113">명령</span><span class="sxs-lookup"><span data-stu-id="b215d-113">Command</span></span> | <span data-ttu-id="b215d-114">참고 사항</span><span class="sxs-lookup"><span data-stu-id="b215d-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b215d-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b215d-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="b215d-116">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b215d-116">Creates a resource group in which all resources are stored.</span></span> | 
| [<span data-ttu-id="b215d-117">새-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="b215d-117">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork)| <span data-ttu-id="b215d-118">Azure Virtual Network 및 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b215d-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="b215d-119">Add-AzureRmVirtualNetworkPeering</span><span class="sxs-lookup"><span data-stu-id="b215d-119">Add-AzureRmVirtualNetworkPeering</span></span>](/powershell/module/azurerm.network/add-azurermvirtualnetworkpeering) | <span data-ttu-id="b215d-120">두 가상 네트워크 간에 피어링을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b215d-120">Creates a peering between two virtual networks.</span></span>  |
| [<span data-ttu-id="b215d-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b215d-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="b215d-122">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="b215d-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b215d-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b215d-123">Next steps</span></span>

<span data-ttu-id="b215d-124">Azure PowerShell hello에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](https://docs.microsoft.com/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="b215d-124">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="b215d-125">추가 네트워킹 PowerShell 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 네트워킹 개요 문서](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="b215d-125">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
