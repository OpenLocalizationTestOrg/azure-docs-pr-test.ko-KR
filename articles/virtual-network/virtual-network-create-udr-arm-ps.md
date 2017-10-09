---
title: "Azure-PowerShell에서에서 라우팅 및 가상 어플라이언스 aaaControl | Microsoft Docs"
description: "자세한 방법을 PowerShell을 사용 하 여 toocontrol 라우팅 및 가상 기기입니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 9582fdaa-249c-4c98-9618-8c30d496940f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.openlocfilehash: b7b8717529eb2cd8b1d28b8ab9c6e21159d14882
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-powershell"></a><span data-ttu-id="203e8-103">PowerShell 사용하여 사용자 정의 경로(UDR) 만들기</span><span class="sxs-lookup"><span data-stu-id="203e8-103">Create User-Defined Routes (UDR) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="203e8-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="203e8-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="203e8-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="203e8-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="203e8-106">템플릿</span><span class="sxs-lookup"><span data-stu-id="203e8-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="203e8-107">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="203e8-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="203e8-108">CLI(클래식)</span><span class="sxs-lookup"><span data-stu-id="203e8-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)


[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="203e8-109">Azure 리소스를 사용 하기 전에 Azure에 현재 두 가지 배포 모델에 중요 한 toounderstand: Azure 리소스 관리자 및 기본 합니다.</span><span class="sxs-lookup"><span data-stu-id="203e8-109">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="203e8-110">Azure 리소스로 작업하기 전에 [배포 모델 및 도구](../azure-resource-manager/resource-manager-deployment-model.md) 를 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="203e8-110">Make sure you understand [deployment models and tools](../azure-resource-manager/resource-manager-deployment-model.md) before you work with any Azure resource.</span></span> <span data-ttu-id="203e8-111">이 문서의 hello 위쪽 hello 탭을 클릭 하 여 다양 한 도구에 대 한 hello 설명서를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="203e8-111">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span>
>

<span data-ttu-id="203e8-112">이 문서에서는 hello 리소스 관리자 배포 모델에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="203e8-112">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="203e8-113">수도 있습니다 [UDRs hello 클래식 배포 모델에서 만들](virtual-network-create-udr-classic-ps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="203e8-113">You can also [create UDRs in hello classic deployment model](virtual-network-create-udr-classic-ps.md).</span></span>

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="203e8-114">위의 hello 시나리오를 기반으로 hello 예제 PowerShell 명령 아래에 이미 만든 단순한 환경 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="203e8-114">hello sample PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="203e8-115">이 문서에 표시 된 대로 toorun hello 명령을 원하는 경우 먼저 hello 테스트 환경을 구축 배포 하 여 [이 서식 파일](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), 클릭 **tooAzure 배포**, 대체 hello 기본 매개 변수 값 필요한 경우, 및의 지침에 따라 hello hello 포털 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="203e8-115">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="203e8-116">Hello UDR hello 프런트 엔드 서브넷에 대 한 만들기</span><span class="sxs-lookup"><span data-stu-id="203e8-116">Create hello UDR for hello front-end subnet</span></span>
<span data-ttu-id="203e8-117">toocreate hello 경로 테이블 및 hello 프런트 엔드 서브넷에 필요한 경로는 위의 단계를 수행 하는 전체 hello hello 시나리오에 따라:</span><span class="sxs-lookup"><span data-stu-id="203e8-117">toocreate hello route table and route needed for hello front-end subnet based on hello scenario above, complete hello following steps:</span></span>

1. <span data-ttu-id="203e8-118">사용 되는 경로 toosend 모든 트래픽이 toohello 백 엔드 서브넷 (192.168.2.0/24) 라우팅된 toobe toohello 만들기 **FW1** 가상 어플라이언스 (192.168.0.4).</span><span class="sxs-lookup"><span data-stu-id="203e8-118">Create a route used toosend all traffic destined toohello back-end subnet (192.168.2.0/24) toobe routed toohello **FW1** virtual appliance (192.168.0.4).</span></span>

    ```powershell
    $route = New-AzureRmRouteConfig -Name RouteToBackEnd `
    -AddressPrefix 192.168.2.0/24 -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

2. <span data-ttu-id="203e8-119">명명 된 경로 테이블 만들기 **UDR 프런트 엔드** hello에 **westus** hello 경로 포함 하는 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="203e8-119">Create a route table named **UDR-FrontEnd** in hello **westus** region that contains hello route.</span></span>

    ```powershell
    $routeTable = New-AzureRmRouteTable -ResourceGroupName TestRG -Location westus `
    -Name UDR-FrontEnd -Route $route
    ```

3. <span data-ttu-id="203e8-120">Hello hello 서브넷이 있는 VNet을 포함 하는 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="203e8-120">Create a variable that contains hello VNet where hello subnet is.</span></span> <span data-ttu-id="203e8-121">이 시나리오에서 hello VNet 라는 **TestVNet**합니다.</span><span class="sxs-lookup"><span data-stu-id="203e8-121">In our scenario, hello VNet is named **TestVNet**.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

4. <span data-ttu-id="203e8-122">연결 hello 경로 테이블 toohello 위에서 만든 **프런트 엔드** 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="203e8-122">Associate hello route table created above toohello **FrontEnd** subnet.</span></span>

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
    -AddressPrefix 192.168.1.0/24 -RouteTable $routeTable
    ```

    > [!WARNING]
    > <span data-ttu-id="203e8-123">위의 hello 명령에 대 한 hello 출력에는 PowerShell를 실행 하는 hello 컴퓨터에만 존재 하는 hello 가상 네트워크 구성 개체에 대 한 hello 콘텐츠를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="203e8-123">hello output for hello command above shows hello content for hello virtual network configuration object, which only exists on hello computer where you are running PowerShell.</span></span> <span data-ttu-id="203e8-124">Toorun hello 필요한 **집합 AzureVirtualNetwork** cmdlet toosave 이러한 설정 tooAzure 합니다.</span><span class="sxs-lookup"><span data-stu-id="203e8-124">You need toorun hello **Set-AzureVirtualNetwork** cmdlet toosave these settings tooAzure.</span></span>
    > 

5. <span data-ttu-id="203e8-125">Azure의 hello 새 서브넷 configuration를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="203e8-125">Save hello new subnet configuration in Azure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="203e8-126">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="203e8-126">Expected output:</span></span>
   
        Name              : TestVNet
        ResourceGroupName : TestRG
        Location          : westus
        Id                : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag              : W/"[Id]"
        ProvisioningState : Succeeded
        Tags              : 
                            Name         Value
                            ===========  =====
                            displayName  VNet 
   
        AddressSpace      : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptions       : {
                              "DnsServers": null
                            }
        NetworkInterfaces : null
        Subnets           : [
                                ...,
                              {
                                "Name": "FrontEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                "AddressPrefix": "192.168.1.0/24",
                                "IpConfigurations": [
                                  {
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB2/ipConfigurations/ipconfig1"
                                  },
                                  {
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConfigurations/ipconfig1"
                                  }
                                ],
                                "NetworkSecurityGroup": {
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                },
                                "RouteTable": {
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-FrontEnd"
                                },
                                "ProvisioningState": "Succeeded"
                              },
                                ...
                            ]    

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="203e8-127">Hello UDR hello 백 엔드 서브넷에 대 한 만들기</span><span class="sxs-lookup"><span data-stu-id="203e8-127">Create hello UDR for hello back-end subnet</span></span>

<span data-ttu-id="203e8-128">toocreate hello 경로 테이블 및 위의 hello 시나리오에 따라 hello 백 엔드 서브넷에 필요한 경로 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="203e8-128">toocreate hello route table and route needed for hello back-end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="203e8-129">사용 되는 경로 toosend 모든 트래픽이 toohello 프런트 엔드 서브넷 (192.168.1.0/24) 라우팅된 toobe toohello 만들기 **FW1** 가상 어플라이언스 (192.168.0.4).</span><span class="sxs-lookup"><span data-stu-id="203e8-129">Create a route used toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toobe routed toohello **FW1** virtual appliance (192.168.0.4).</span></span>

    ```powershell
    $route = New-AzureRmRouteConfig -Name RouteToFrontEnd `
    -AddressPrefix 192.168.1.0/24 -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

2. <span data-ttu-id="203e8-130">명명 된 경로 테이블 만들기 **UDR 백 엔드** hello에 **uswest** 위에서 만든 hello 경로 포함 하는 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="203e8-130">Create a route table named **UDR-BackEnd** in hello **uswest** region that contains hello route created above.</span></span>

    ```
    $routeTable = New-AzureRmRouteTable -ResourceGroupName TestRG -Location westus `
    -Name UDR-BackEnd -Route $route
    ```

3. <span data-ttu-id="203e8-131">연결 hello 경로 테이블 toohello 위에서 만든 **백 엔드** 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="203e8-131">Associate hello route table created above toohello **BackEnd** subnet.</span></span>

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name BackEnd `
    -AddressPrefix 192.168.2.0/24 -RouteTable $routeTable
    ```

4. <span data-ttu-id="203e8-132">Azure의 hello 새 서브넷 configuration를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="203e8-132">Save hello new subnet configuration in Azure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="203e8-133">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="203e8-133">Expected output:</span></span>
   
        Name              : TestVNet
        ResourceGroupName : TestRG
        Location          : westus
        Id                : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag              : W/"[Id]"
        ProvisioningState : Succeeded
        Tags              : 
                            Name         Value
                            ===========  =====
                            displayName  VNet 
   
        AddressSpace      : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptions       : {
                              "DnsServers": null
                            }
        NetworkInterfaces : null
        Subnets           : [
                              ...,
                              {
                                "Name": "BackEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                "AddressPrefix": "192.168.2.0/24",
                                "IpConfigurations": [
                                  {
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICSQL2/ipConfigurations/ipconfig1"
                                  },
                                  {
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICSQL1/ipConfigurations/ipconfig1"
                                  }
                                ],
                                "NetworkSecurityGroup": {
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BacEnd"
                                },
                                "RouteTable": {
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd"
                                },
                                "ProvisioningState": "Succeeded"
                              }
                            ]

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="203e8-134">FW1에서 IP 전달을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="203e8-134">Enable IP forwarding on FW1</span></span>
<span data-ttu-id="203e8-135">hello에서 사용 하는 NIC에 IP 전달을 tooenable **FW1**, 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="203e8-135">tooenable IP forwarding in hello NIC used by **FW1**, follow hello steps below.</span></span>

1. <span data-ttu-id="203e8-136">NIC FW1에서 사용 하는 hello에 대 한 hello 설정을 포함 하는 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="203e8-136">Create a variable that contains hello settings for hello NIC used by FW1.</span></span> <span data-ttu-id="203e8-137">이 시나리오에서 hello NIC 라는 **NICFW1**합니다.</span><span class="sxs-lookup"><span data-stu-id="203e8-137">In our scenario, hello NIC is named **NICFW1**.</span></span>

    ```powershell
    $nicfw1 = Get-AzureRmNetworkInterface -ResourceGroupName TestRG -Name NICFW1
    ```

2. <span data-ttu-id="203e8-138">IP 전달을 사용 하도록 설정 하 고 hello NIC 설정을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="203e8-138">Enable IP forwarding, and save hello NIC settings.</span></span>

    ```powershell
    $nicfw1.EnableIPForwarding = 1
    Set-AzureRmNetworkInterface -NetworkInterface $nicfw1
    ```
   
    <span data-ttu-id="203e8-139">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="203e8-139">Expected output:</span></span>
   
        Name                 : NICFW1
        ResourceGroupName    : TestRG
        Location             : westus
        Id                   : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICFW1
        Etag                 : W/"[Id]"
        ProvisioningState    : Succeeded
        Tags                 : 
                               Name         Value                  
                               ===========  =======================
                               displayName  NetworkInterfaces - DMZ
   
        VirtualMachine       : {
                                 "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/FW1"
                               }
        IpConfigurations     : [
                                 {
                                   "Name": "ipconfig1",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICFW1/ipConfigurations/ipconfig1",
                                   "PrivateIpAddress": "192.168.0.4",
                                   "PrivateIpAllocationMethod": "Static",
                                   "Subnet": {
                                     "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/DMZ"
                                   },
                                   "PublicIpAddress": {
                                     "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/PIPFW1"
                                   },
                                   "LoadBalancerBackendAddressPools": [],
                                   "LoadBalancerInboundNatRules": [],
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]
        DnsSettings          : {
                                 "DnsServers": [],
                                 "AppliedDnsServers": [],
                                 "InternalDnsNameLabel": null,
                                 "InternalFqdn": null
                               }
        EnableIPForwarding   : True
        NetworkSecurityGroup : null
        Primary              : True

