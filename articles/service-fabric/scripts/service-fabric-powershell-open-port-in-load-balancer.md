---
title: "PowerShell 스크립트 샘플-부하 분산 장치에서 응용 프로그램 열기 포트 aaaAzure | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플-서비스 패브릭 응용 프로그램에 대 한 hello Azure 부하 분산 장치에서 포트 열기."
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
ms.openlocfilehash: 6acb28942851dce63f89f7de362b7cf1dc7b1fee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="open-an-application-port-in-hello-azure-load-balancer"></a><span data-ttu-id="baa4e-103">Hello Azure 부하 분산 장치에 응용 프로그램 포트 열기</span><span class="sxs-lookup"><span data-stu-id="baa4e-103">Open an application port in hello Azure load balancer</span></span>

<span data-ttu-id="baa4e-104">Azure에서 실행 되는 서비스 패브릭 응용 프로그램은 hello Azure 부하 분산 장치 뒤에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="baa4e-104">A Service Fabric application running in Azure sits behind hello Azure load balancer.</span></span> <span data-ttu-id="baa4e-105">이 샘플 스크립트는 Service Fabric 응용 프로그램이 외부 클라이언트와 통신할 수 있도록 Azure Load Balancer에서 포트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="baa4e-105">This sample script opens a port in an Azure load balancer so that a Service Fabric application can communicate with external clients.</span></span> <span data-ttu-id="baa4e-106">필요에 따라 hello 매개 변수를 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="baa4e-106">Customize hello parameters as needed.</span></span> 

<span data-ttu-id="baa4e-107">필요한 경우 hello로 hello 서비스 패브릭 PowerShell 모듈을 설치 [서비스 패브릭 SDK](../service-fabric-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="baa4e-107">If needed, install hello Service Fabric PowerShell module with hello [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="baa4e-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="baa4e-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/open-port-in-load-balancer/open-port-in-load-balancer.ps1 "Open a port in hello load balancer")]

## <a name="script-explanation"></a><span data-ttu-id="baa4e-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="baa4e-109">Script explanation</span></span>

<span data-ttu-id="baa4e-110">이 스크립트 명령 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="baa4e-110">This script uses hello following commands.</span></span> <span data-ttu-id="baa4e-111">Hello 테이블 링크 toocommand 특정 설명서에서 각 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="baa4e-111">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="baa4e-112">명령</span><span class="sxs-lookup"><span data-stu-id="baa4e-112">Command</span></span> | <span data-ttu-id="baa4e-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="baa4e-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="baa4e-114">Get-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="baa4e-114">Get-AzureRmResource</span></span>](/powershell/module/azurerm.resources/get-azurermresource) | <span data-ttu-id="baa4e-115">Azure 리소스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="baa4e-115">Gets an Azure resource.</span></span>  |
| [<span data-ttu-id="baa4e-116">Get-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="baa4e-116">Get-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/get-azurermloadbalancer) | <span data-ttu-id="baa4e-117">Hello Azure 부하 분산 장치를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="baa4e-117">Gets hello Azure load balancer.</span></span> |
| [<span data-ttu-id="baa4e-118">Add-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="baa4e-118">Add-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig) | <span data-ttu-id="baa4e-119">프로브 구성 tooa 부하 분산 장치를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="baa4e-119">Adds a probe configuration tooa load balancer.</span></span>|
| [<span data-ttu-id="baa4e-120">Get-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="baa4e-120">Get-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/get-azurermloadbalancerprobeconfig) | <span data-ttu-id="baa4e-121">Load Balancer에 대한 프로브 구성을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="baa4e-121">Gets a probe configuration for a load balancer.</span></span> |
| [<span data-ttu-id="baa4e-122">Add-AzureRmLoadBalancerRuleConfig</span><span class="sxs-lookup"><span data-stu-id="baa4e-122">Add-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig) | <span data-ttu-id="baa4e-123">규칙 구성 tooa 부하 분산 장치를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="baa4e-123">Adds a rule configuration tooa load balancer.</span></span> |
| [<span data-ttu-id="baa4e-124">Set-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="baa4e-124">Set-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/set-azurermloadbalancer) | <span data-ttu-id="baa4e-125">집합에는 부하 분산 장치에 대 한 목표 상태를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="baa4e-125">Sets hello goal state for a load balancer.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="baa4e-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="baa4e-126">Next steps</span></span>

<span data-ttu-id="baa4e-127">Hello Azure PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="baa4e-127">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="baa4e-128">Azure Service Fabric에 대 한 추가 Powershell 샘플 hello에서 확인할 수 있습니다 [Azure PowerShell 샘플](../service-fabric-powershell-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="baa4e-128">Additional Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
