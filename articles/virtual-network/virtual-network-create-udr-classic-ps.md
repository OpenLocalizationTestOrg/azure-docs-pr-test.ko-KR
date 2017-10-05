---
title: "Azure Virtual Network에서 라우팅 제어 - PowerShell - 클래식 | Microsoft Docs"
description: "PowerShell을 사용하여 VNet에서 라우팅을 제어하는 방법 알아보기 | 클래식"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: d8d07c16-cbe5-4536-acd6-870269346fe3
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: e9564d223cb85529f1fa97bc398d35c6debcedae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-powershell"></a><span data-ttu-id="45297-103">PowerShell 사용하여 라우팅 제어 및 가상 어플라이언스(클래식) 사용</span><span class="sxs-lookup"><span data-stu-id="45297-103">Control routing and use virtual appliances (classic) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="45297-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="45297-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="45297-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="45297-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="45297-106">템플릿</span><span class="sxs-lookup"><span data-stu-id="45297-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="45297-107">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="45297-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="45297-108">CLI(클래식)</span><span class="sxs-lookup"><span data-stu-id="45297-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="45297-109">Azure 리소스로 작업하기 전에 Azure에는 현재 Azure Resource Manager와 클래식 모드의 두 가지 배포 모델이 있다는 것을 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45297-109">Before you work with Azure resources, it's important to understand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="45297-110">Azure 리소스로 작업하기 전에 [배포 모델 및 도구](../azure-resource-manager/resource-manager-deployment-model.md) 를 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45297-110">Make sure you understand [deployment models and tools](../azure-resource-manager/resource-manager-deployment-model.md) before you work with any Azure resource.</span></span> <span data-ttu-id="45297-111">이 문서의 윗부분에 있는 옵션을 선택하여 다양한 도구에 대한 설명서를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45297-111">You can view the documentation for different tools by selecting an option at the top of this article.</span></span> <span data-ttu-id="45297-112">이 문서에서는 클래식 배포 모델에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="45297-112">This article covers the classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="45297-113">아래 샘플 Azure PowerShell 명령에는 위의 시나리오를 기반으로 이미 만들어져 있는 단순한 환경이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="45297-113">The sample Azure PowerShell commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="45297-114">이 문서에 표시된 대로 명령을 실행하려는 경우 먼저 [PowerShell을 사용하여 VNet(클래식) 만들기](virtual-networks-create-vnet-classic-netcfg-ps.md)에 표시된 환경을 구축합니다.</span><span class="sxs-lookup"><span data-stu-id="45297-114">If you want to run the commands as they are displayed in this document, create the environment shown in [create a VNet (classic) using PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-the-udr-for-the-front-end-subnet"></a><span data-ttu-id="45297-115">프런트 엔드 서브넷에 대한 UDR 만들기</span><span class="sxs-lookup"><span data-stu-id="45297-115">Create the UDR for the front end subnet</span></span>
<span data-ttu-id="45297-116">위의 시나리오에 따라 필요한 경로 테이블 및 경로를 만들려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="45297-116">To create the route table and route needed for the front end subnet based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="45297-117">다음 명령을 실행하여 프런트 엔드 서브넷에 대한 경로 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="45297-117">Run the following command to create a route table for the front-end subnet:</span></span>

    ```powershell
    New-AzureRouteTable -Name UDR-FrontEnd -Location uswest `
    -Label "Route table for front end subnet"
    ```

2. <span data-ttu-id="45297-118">다음 명령을 실행하여 경로 테이블에 경로를 만들고 백 엔드 서브넷(192.168.2.0/24)으로 보내진 모든 트래픽을 **FW1** VM(192.168.0.4)으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="45297-118">Run the following command to create a route in the route table to send all traffic destined to the back-end subnet (192.168.2.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```powershell
    Get-AzureRouteTable UDR-FrontEnd `
    |Set-AzureRoute -RouteName RouteToBackEnd -AddressPrefix 192.168.2.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. <span data-ttu-id="45297-119">다음 명령을 실행하여 경로 테이블을 **FrontEnd** 서브넷에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="45297-119">Run the following command to associate the route table with the **FrontEnd** subnet:</span></span>

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName FrontEnd `
    -RouteTableName UDR-FrontEnd
    ```

## <a name="create-the-udr-for-the-back-end-subnet"></a><span data-ttu-id="45297-120">백 엔드 서브넷에 대한 UDR 만들기</span><span class="sxs-lookup"><span data-stu-id="45297-120">Create the UDR for the back-end subnet</span></span>
<span data-ttu-id="45297-121">시나리오에 따라 백 엔드 서브넷에 필요한 경로 테이블 및 경로를 만들려면 다음 단계를 마칩니다.</span><span class="sxs-lookup"><span data-stu-id="45297-121">To create the route table and route needed for the back end subnet based on the scenario, complete the following steps:</span></span>

1. <span data-ttu-id="45297-122">다음 명령을 실행하여 백 엔드 서브넷에 대한 경로 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="45297-122">Run the following command to create a route table for the back-end subnet:</span></span>

    ```powershell
    New-AzureRouteTable -Name UDR-BackEnd `
    -Location uswest `
    -Label "Route table for back end subnet"
    ```

2. <span data-ttu-id="45297-123">다음 명령을 실행하여 경로 테이블에 경로를 만들고 프런트 엔드 서브넷(192.168.1.0/24)으로 보내진 모든 트래픽을 **FW1** VM(192.168.0.4)으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="45297-123">Run the following command to create a route in the route table to send all traffic destined to the front-end subnet (192.168.1.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```powershell
    Get-AzureRouteTable UDR-BackEnd
    | Set-AzureRoute `
    -RouteName RouteToFrontEnd `
    -AddressPrefix 192.168.1.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. <span data-ttu-id="45297-124">다음 명령을 실행하여 경로 테이블을 **BackEnd** 서브넷에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="45297-124">Run the following command to associate the route table with the **BackEnd** subnet:</span></span>

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName BackEnd `
    -RouteTableName UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-the-fw1-vm"></a><span data-ttu-id="45297-125">FW1 VM에서 IP 전달을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="45297-125">Enable IP forwarding on the FW1 VM</span></span>

<span data-ttu-id="45297-126">FW1 VM에 IP 전달을 사용하도록 설정하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="45297-126">To enable IP forwarding in the FW1 VM, complete the following steps:</span></span>

1. <span data-ttu-id="45297-127">다음 명령을 실행하여 IP 전달 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="45297-127">Run the following command to check the status of IP forwarding:</span></span>

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Get-AzureIPForwarding
    ```

2. <span data-ttu-id="45297-128">다음 명령을 실행하여 *FW1* VM에 대한 IP 전달을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="45297-128">Run the following command to enable IP forwarding for the *FW1* VM:</span></span>

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Set-AzureIPForwarding -Enable
    ```
