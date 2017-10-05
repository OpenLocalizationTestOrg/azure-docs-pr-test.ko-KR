---
title: "인터넷 연결 부하 분산 장치 만들기 - Azure PowerShell 클래식 | Microsoft Docs"
description: "PowerShell을 사용하여 클래식 모드에서 인터넷 연결 부하 분산 장치를 만드는 방법에 대해 알아봅니다."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 73e8bfa4-8086-4ef0-9e35-9e00b24be319
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 1a41f3ba199fb692c111ea6a40ddb09605f91da2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-powershell"></a><span data-ttu-id="da070-103">PowerShell에서 인터넷 연결 부하 분산 장치(클래식) 만들기 시작</span><span class="sxs-lookup"><span data-stu-id="da070-103">Get started creating an Internet facing load balancer (classic) in PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="da070-104">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="da070-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="da070-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="da070-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="da070-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="da070-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="da070-107">Azure 클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="da070-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="da070-108">Azure 리소스로 작업하기 전에 Azure에는 현재 Azure Resource Manager와 클래식 모드의 두 가지 배포 모델이 있다는 것을 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da070-108">Before you work with Azure resources, it's important to understand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="da070-109">Azure 리소스로 작업하기 전에 [배포 모델 및 도구](../azure-classic-rm.md) 를 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da070-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="da070-110">이 문서의 윗부분에 있는 탭을 클릭하여 다양한 도구에 대한 설명서를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da070-110">You can view the documentation for different tools by clicking the tabs at the top of this article.</span></span> <span data-ttu-id="da070-111">이 문서에서는 클래식 배포 모델에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="da070-111">This article covers the classic deployment model.</span></span> <span data-ttu-id="da070-112">또한 [Azure 리소스 관리자를 사용하여 인터넷 연결 부하 분산 장치를 만드는 방법을 배울 수 있습니다](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="da070-112">You can also [Learn how to create an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-load-balancer-using-powershell"></a><span data-ttu-id="da070-113">PowerShell을 사용하여 부하 분산 장치 설정</span><span class="sxs-lookup"><span data-stu-id="da070-113">Set up load balancer using PowerShell</span></span>

<span data-ttu-id="da070-114">PowerShell을 사용하여 부하 분산 장치를 설정하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="da070-114">To set up a load balancer using powershell, follow the steps below:</span></span>

1. <span data-ttu-id="da070-115">Azure PowerShell을 처음 사용하는 경우 [Azure PowerShell을 설치 및 구성하는 방법](/powershell/azure/overview) 을 참조하고 지침을 끝까지 따르면서 Azure에 로그인하고 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="da070-115">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azure/overview) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="da070-116">가상 컴퓨터를 만든 후 PowerShell cmdlet을 사용하여 동일한 클라우드 서비스 내에서 가상 컴퓨터로 부하 분산 장치를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da070-116">After creating a virtual machine, you can use PowerShell cmdlets to add a load balancer to a virtual machine within the same cloud service.</span></span>

<span data-ttu-id="da070-117">다음 예제에서는 클라우드 서비스 "webfarm"라고 하는 부하 분산 장치 집합을 클라우드 서비스 "mytestcloud"(또는 myctestcloud.cloudapp.net)에 추가하여, 부하 분산 장치의 끝점을 "web1" 및 "web2"라는 가상 컴퓨터에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="da070-117">In the following example you will add a load balancer set called "webfarm" to cloud service "mytestcloud" (or myctestcloud.cloudapp.net) , adding the endpoints for the load balancer to virtual machines named "web1" and "web2".</span></span> <span data-ttu-id="da070-118">부하 분산 장치는 포트 80에서 트래픽을 받고 TCP를 사용하여 로컬 끝점(이 경우 포트 80)에서 정의된 가상 컴퓨터들 간의 부하를 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="da070-118">The load balancer receives network traffic on port 80 and load balances between the virtual machines defined by the local endpoint (in this case port 80) using TCP.</span></span>

### <a name="step-1"></a><span data-ttu-id="da070-119">1단계</span><span class="sxs-lookup"><span data-stu-id="da070-119">Step 1</span></span>

<span data-ttu-id="da070-120">첫 번째 VM "web1"을 위한 부하 분산 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="da070-120">Create a load balanced endpoint for the first VM "web1"</span></span>

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

### <a name="step-2"></a><span data-ttu-id="da070-121">2단계</span><span class="sxs-lookup"><span data-stu-id="da070-121">Step 2</span></span>

<span data-ttu-id="da070-122">동일한 부하 분산 장치 집합 이름을 사용하여 두 번째 VM "web2"를 위한 다른 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="da070-122">Create another endpoint for the second VM  "web2" using the same load balancer set name</span></span>

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web2" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

## <a name="remove-a-virtual-machine-from-a-load-balancer"></a><span data-ttu-id="da070-123">부하 분산 장치에서 가상 컴퓨터 제거</span><span class="sxs-lookup"><span data-stu-id="da070-123">Remove a virtual machine from a load balancer</span></span>

<span data-ttu-id="da070-124">Remove-AzureEndpoint를 사용하여 부하 분산 장치에서 가상 컴퓨터 끝점을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da070-124">You can use Remove-AzureEndpoint to remove a virtual machine endpoint from the load balancer</span></span>

```powershell
Get-azureVM -ServiceName mytestcloud  -Name web1 |Remove-AzureEndpoint -Name httpin | Update-AzureVM
```

## <a name="next-steps"></a><span data-ttu-id="da070-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="da070-125">Next steps</span></span>

<span data-ttu-id="da070-126">[내부 부하 분산 장치를 시작](load-balancer-get-started-ilb-classic-ps.md)하고 특정 부하 분산 장치 네트워크 트래픽 동작에 대한 [배포 모드](load-balancer-distribution-mode.md) 유형을 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da070-126">You can also [get started creating an internal load balancer](load-balancer-get-started-ilb-classic-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for a specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="da070-127">응용 프로그램이 부하 분산 장치 뒤의 서버에 대한 연결을 유지해야 하는 경우 [부하 분산 장치에 대한 유휴 TCP 시간 제한 설정](load-balancer-tcp-idle-timeout.md)에 대해 자세히 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da070-127">If your application needs to keep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="da070-128">Azure 부하 분산 장치를 사용하는 경우 유휴 연결 동작에 대해 알아보는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="da070-128">It will help to learn about idle connection behavior when you are using Azure Load Balancer.</span></span>
