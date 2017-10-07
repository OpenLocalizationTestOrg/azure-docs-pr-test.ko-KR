---
title: "Azure 가상 네트워크-PowerShell-클래식에서 aaaControl 라우팅을 | Microsoft Docs"
description: "자세한 내용은 방법 toocontrol PowerShell을 사용 하 여 Vnet에 라우팅 | 클래식"
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
ms.openlocfilehash: 36edf263fb434d5fb13310d4324da20e57f016a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-powershell"></a><span data-ttu-id="7f9e6-103">PowerShell 사용하여 라우팅 제어 및 가상 어플라이언스(클래식) 사용</span><span class="sxs-lookup"><span data-stu-id="7f9e6-103">Control routing and use virtual appliances (classic) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7f9e6-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7f9e6-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="7f9e6-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7f9e6-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="7f9e6-106">템플릿</span><span class="sxs-lookup"><span data-stu-id="7f9e6-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="7f9e6-107">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="7f9e6-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="7f9e6-108">CLI(클래식)</span><span class="sxs-lookup"><span data-stu-id="7f9e6-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="7f9e6-109">Azure 리소스를 사용 하기 전에 Azure에 현재 두 가지 배포 모델에 중요 한 toounderstand: Azure 리소스 관리자 및 기본 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f9e6-109">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="7f9e6-110">Azure 리소스로 작업하기 전에 [배포 모델 및 도구](../azure-resource-manager/resource-manager-deployment-model.md) 를 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f9e6-110">Make sure you understand [deployment models and tools](../azure-resource-manager/resource-manager-deployment-model.md) before you work with any Azure resource.</span></span> <span data-ttu-id="7f9e6-111">이 문서의 hello 위쪽에 옵션을 선택 하 여 다양 한 도구에 대 한 hello 설명서를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f9e6-111">You can view hello documentation for different tools by selecting an option at hello top of this article.</span></span> <span data-ttu-id="7f9e6-112">이 문서에서는 hello 클래식 배포 모델에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f9e6-112">This article covers hello classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="7f9e6-113">위의 hello 시나리오를 기반으로 hello 샘플 Azure PowerShell 명령 아래에 이미 만든 단순한 환경 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f9e6-113">hello sample Azure PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="7f9e6-114">이 문서에 표시 된 대로 toorun hello 명령을 하려는 경우 만들 hello 환경에 표시 된 [PowerShell을 사용 하 여 VNet (클래식)을 만들](virtual-networks-create-vnet-classic-netcfg-ps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7f9e6-114">If you want toorun hello commands as they are displayed in this document, create hello environment shown in [create a VNet (classic) using PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="7f9e6-115">Hello UDR hello 프런트 엔드 서브넷에 대 한 만들기</span><span class="sxs-lookup"><span data-stu-id="7f9e6-115">Create hello UDR for hello front end subnet</span></span>
<span data-ttu-id="7f9e6-116">toocreate hello 경로 테이블 및 필요한 위의 hello 시나리오에 따라 hello 프런트 엔드 서브넷에 대 한 경로 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f9e6-116">toocreate hello route table and route needed for hello front end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="7f9e6-117">다음 명령은 toocreate hello hello 프런트 엔드 서브넷에 대 한 경로 테이블을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f9e6-117">Run hello following command toocreate a route table for hello front-end subnet:</span></span>

    ```powershell
    New-AzureRouteTable -Name UDR-FrontEnd -Location uswest `
    -Label "Route table for front end subnet"
    ```

2. <span data-ttu-id="7f9e6-118">모든 트래픽이 toohello 백 엔드 서브넷 (192.168.2.0/24) toohello 명령 toocreate hello 경로 테이블 toosend에서 경로 따라 hello 실행 **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="7f9e6-118">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello back-end subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```powershell
    Get-AzureRouteTable UDR-FrontEnd `
    |Set-AzureRoute -RouteName RouteToBackEnd -AddressPrefix 192.168.2.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. <span data-ttu-id="7f9e6-119">실행 hello 명령 tooassociate hello 경로 테이블 hello로 다음 **프런트 엔드** 서브넷:</span><span class="sxs-lookup"><span data-stu-id="7f9e6-119">Run hello following command tooassociate hello route table with hello **FrontEnd** subnet:</span></span>

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName FrontEnd `
    -RouteTableName UDR-FrontEnd
    ```

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="7f9e6-120">Hello UDR hello 백 엔드 서브넷에 대 한 만들기</span><span class="sxs-lookup"><span data-stu-id="7f9e6-120">Create hello UDR for hello back-end subnet</span></span>
<span data-ttu-id="7f9e6-121">서브넷 hello 시나리오에 따라 종료 toocreate hello 경로 테이블 및 경로 hello 백에 필요한 단계를 수행 하는 hello를 완료 하십시오.</span><span class="sxs-lookup"><span data-stu-id="7f9e6-121">toocreate hello route table and route needed for hello back end subnet based on hello scenario, complete hello following steps:</span></span>

1. <span data-ttu-id="7f9e6-122">다음 명령은 toocreate hello hello 백 엔드 서브넷에 대 한 경로 테이블을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f9e6-122">Run hello following command toocreate a route table for hello back-end subnet:</span></span>

    ```powershell
    New-AzureRouteTable -Name UDR-BackEnd `
    -Location uswest `
    -Label "Route table for back end subnet"
    ```

2. <span data-ttu-id="7f9e6-123">모든 트래픽이 toohello 프런트 엔드 서브넷 (192.168.1.0/24) toohello 명령 toocreate hello 경로 테이블 toosend에서 경로 따라 hello 실행 **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="7f9e6-123">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```powershell
    Get-AzureRouteTable UDR-BackEnd
    | Set-AzureRoute `
    -RouteName RouteToFrontEnd `
    -AddressPrefix 192.168.1.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. <span data-ttu-id="7f9e6-124">실행 hello 명령 tooassociate hello 경로 테이블 hello로 다음 **백 엔드** 서브넷:</span><span class="sxs-lookup"><span data-stu-id="7f9e6-124">Run hello following command tooassociate hello route table with hello **BackEnd** subnet:</span></span>

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName BackEnd `
    -RouteTableName UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-hello-fw1-vm"></a><span data-ttu-id="7f9e6-125">Hello FW1 VM에 IP 전달을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="7f9e6-125">Enable IP forwarding on hello FW1 VM</span></span>

<span data-ttu-id="7f9e6-126">hello FW1 VM을 단계를 수행 하는 전체 hello에에서 tooenable IP 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f9e6-126">tooenable IP forwarding in hello FW1 VM, complete hello following steps:</span></span>

1. <span data-ttu-id="7f9e6-127">다음의 IP 전달 명령 toocheck hello 상태 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f9e6-127">Run hello following command toocheck hello status of IP forwarding:</span></span>

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Get-AzureIPForwarding
    ```

2. <span data-ttu-id="7f9e6-128">실행된 hello 다음 명령은 hello에 대 한 IP 전달 tooenable *FW1* VM:</span><span class="sxs-lookup"><span data-stu-id="7f9e6-128">Run hello following command tooenable IP forwarding for hello *FW1* VM:</span></span>

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Set-AzureIPForwarding -Enable
    ```
