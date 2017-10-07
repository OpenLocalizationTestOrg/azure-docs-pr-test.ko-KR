---
title: "PowerShell 스크립트 샘플-aaaAzure 다층 계층 응용 프로그램에 대 한 네트워크 만들기 | Microsoft Docs"
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
ms.openlocfilehash: 46d6d16dc5dbc8be467359f31346f017727b1abe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a><span data-ttu-id="396a1-103">다중 계층 응용 프로그램을 위한 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="396a1-103">Create a network for multi-tier applications</span></span>

<span data-ttu-id="396a1-104">이 스크립트 샘플은 프런트 엔드 및 백 엔드 서브넷이 있는 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="396a1-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="396a1-105">트래픽 toohello 프런트 엔드 서브넷은 제한 된 tooHTTP 및 SSH, 트래픽 toohello 하는 동안 백 엔드 서브넷은 제한 된 tooMySQL, 3306 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="396a1-105">Traffic toohello front-end subnet is limited tooHTTP and SSH, while traffic toohello back-end subnet is limited tooMySQL, port 3306.</span></span> <span data-ttu-id="396a1-106">Hello 스크립트를 실행 한 후 웹 서버 및 MySQL 소프트웨어를 배포할 수 있는 각 서브넷에 각각 하나씩 두 개의 가상 컴퓨터가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="396a1-106">After running hello script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span></span>

<span data-ttu-id="396a1-107">필요한 경우 설치 명령 hello를 사용 하 여 Azure PowerShell hello 있는 hello [Azure PowerShell 가이드](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), 한 다음 실행 `Login-AzureRmAccount` toocreate Azure와의 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="396a1-107">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="396a1-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="396a1-108">Sample script</span></span>


[!code-powershell[main](../../../powershell_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.ps1  "Virtual network for multi-tier application")]

## <a name="clean-up-deployment"></a><span data-ttu-id="396a1-109">배포 정리</span><span class="sxs-lookup"><span data-stu-id="396a1-109">Clean up deployment</span></span> 

<span data-ttu-id="396a1-110">Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="396a1-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="396a1-111">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="396a1-111">Script explanation</span></span>

<span data-ttu-id="396a1-112">이 스크립트는 리소스 그룹, 가상 네트워크 및 네트워크 보안 그룹 명령 toocreate 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="396a1-112">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="396a1-113">Hello 테이블 링크 toocommand 특정 설명서에서 각 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="396a1-113">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="396a1-114">명령</span><span class="sxs-lookup"><span data-stu-id="396a1-114">Command</span></span> | <span data-ttu-id="396a1-115">참고 사항</span><span class="sxs-lookup"><span data-stu-id="396a1-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="396a1-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="396a1-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="396a1-117">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="396a1-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="396a1-118">새-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="396a1-118">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="396a1-119">Azure 가상 네트워크 및 프런트 엔드 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="396a1-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="396a1-120">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="396a1-120">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="396a1-121">백 엔드 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="396a1-121">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="396a1-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="396a1-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="396a1-123">Hello 인터넷에서에서 공용 IP 주소 tooaccess hello VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="396a1-123">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="396a1-124">새-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="396a1-124">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="396a1-125">가상 네트워크 인터페이스를 만들고 toohello 가상 네트워크의 프런트 엔드 및 백 엔드 서브넷에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="396a1-125">Creates virtual network interfaces and attaches them toohello virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="396a1-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="396a1-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="396a1-127">네트워크 보안 그룹 (NSG) 관련된 toohello 프런트 엔드 및 백 엔드 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="396a1-127">Creates network security groups (NSG) that are associated toohello front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="396a1-128">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="396a1-128">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) |<span data-ttu-id="396a1-129">NSG 규칙을 허용 하거나 차단할 toospecific 서브넷 특정 포트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="396a1-129">Creates NSG rules that allow or block specific ports toospecific subnets.</span></span> |
| [<span data-ttu-id="396a1-130">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="396a1-130">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="396a1-131">가상 컴퓨터를 만들고 NIC tooeach VM을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="396a1-131">Creates virtual machines and attaches a NIC tooeach VM.</span></span> <span data-ttu-id="396a1-132">이 명령은 가상 컴퓨터 이미지 toouse hello와 관리 자격 증명에도 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="396a1-132">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="396a1-133">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="396a1-133">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="396a1-134">리소스 그룹 및 이 그룹에 속한 모든 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="396a1-134">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="396a1-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="396a1-135">Next steps</span></span>

<span data-ttu-id="396a1-136">Azure PowerShell hello에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](https://docs.microsoft.com/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="396a1-136">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="396a1-137">추가 네트워킹 PowerShell 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 네트워킹 개요 문서](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="396a1-137">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
