---
title: "Azure PowerShell 스크립트 샘플 - Load Balancer에서 응용 프로그램 포트 열기 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - Service Fabric 응용 프로그램에 대한 Azure Load Balancer에서 응용 프로그램 포트 열기"
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 2958bdef0889076249918608c04c66678fa80b97
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="open-an-application-port-in-the-azure-load-balancer"></a><span data-ttu-id="70db5-103">Azure Load Balancer에서 응용 프로그램 포트 열기</span><span class="sxs-lookup"><span data-stu-id="70db5-103">Open an application port in the Azure load balancer</span></span>

<span data-ttu-id="70db5-104">Azure에서 실행되는 Service Fabric 응용 프로그램은 Azure Load Balancer 뒤에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70db5-104">A Service Fabric application running in Azure sits behind the Azure load balancer.</span></span> <span data-ttu-id="70db5-105">이 샘플 스크립트는 Service Fabric 응용 프로그램이 외부 클라이언트와 통신할 수 있도록 Azure Load Balancer에서 포트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="70db5-105">This sample script opens a port in an Azure load balancer so that a Service Fabric application can communicate with external clients.</span></span> <span data-ttu-id="70db5-106">필요에 따라 매개 변수를 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="70db5-106">Customize the parameters as needed.</span></span> 

<span data-ttu-id="70db5-107">필요한 경우 [Service Fabric SDK](../service-fabric-get-started.md)를 사용하여 Service Fabric PowerShell 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="70db5-107">If needed, install the Service Fabric PowerShell module with the [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="70db5-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="70db5-108">Sample script</span></span>

<span data-ttu-id="70db5-109">[!code-powershell[main](../../../powershell_scripts/service-fabric/open-port-in-load-balancer/open-port-in-load-balancer.ps1 "Load Balancer에서 포트 열기")]</span><span class="sxs-lookup"><span data-stu-id="70db5-109">[!code-powershell[main](../../../powershell_scripts/service-fabric/open-port-in-load-balancer/open-port-in-load-balancer.ps1 "Open a port in the load balancer")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="70db5-110">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="70db5-110">Script explanation</span></span>

<span data-ttu-id="70db5-111">이 스크립트는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="70db5-111">This script uses the following commands.</span></span> <span data-ttu-id="70db5-112">표에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="70db5-112">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="70db5-113">명령</span><span class="sxs-lookup"><span data-stu-id="70db5-113">Command</span></span> | <span data-ttu-id="70db5-114">참고 사항</span><span class="sxs-lookup"><span data-stu-id="70db5-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="70db5-115">Get-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="70db5-115">Get-AzureRmResource</span></span>](/powershell/module/azurerm.resources/get-azurermresource) | <span data-ttu-id="70db5-116">Azure 리소스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="70db5-116">Gets an Azure resource.</span></span>  |
| [<span data-ttu-id="70db5-117">Get-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="70db5-117">Get-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/get-azurermloadbalancer) | <span data-ttu-id="70db5-118">Azure Load Balancer를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="70db5-118">Gets the Azure load balancer.</span></span> |
| [<span data-ttu-id="70db5-119">Add-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="70db5-119">Add-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig) | <span data-ttu-id="70db5-120">Load Balancer에 프로브 구성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="70db5-120">Adds a probe configuration to a load balancer.</span></span>|
| [<span data-ttu-id="70db5-121">Get-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="70db5-121">Get-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/get-azurermloadbalancerprobeconfig) | <span data-ttu-id="70db5-122">Load Balancer에 대한 프로브 구성을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="70db5-122">Gets a probe configuration for a load balancer.</span></span> |
| [<span data-ttu-id="70db5-123">Add-AzureRmLoadBalancerRuleConfig</span><span class="sxs-lookup"><span data-stu-id="70db5-123">Add-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig) | <span data-ttu-id="70db5-124">Load Balancer에 규칙 구성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="70db5-124">Adds a rule configuration to a load balancer.</span></span> |
| [<span data-ttu-id="70db5-125">Set-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="70db5-125">Set-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/set-azurermloadbalancer) | <span data-ttu-id="70db5-126">Load Balancer에 대한 목표 상태를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="70db5-126">Sets the goal state for a load balancer.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="70db5-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="70db5-127">Next steps</span></span>

<span data-ttu-id="70db5-128">Azure PowerShell 모듈에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="70db5-128">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="70db5-129">Azure Service Fabric에 대한 추가 PowerShell 샘플은 [Azure PowerShell 샘플](../service-fabric-powershell-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70db5-129">Additional Powershell samples for Azure Service Fabric can be found in the [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
