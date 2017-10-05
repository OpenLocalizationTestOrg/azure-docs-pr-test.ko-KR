---
title: "가상 네트워크 만들기 - Azure PowerShell | Microsoft Docs"
description: "PowerShell을 사용하여 가상 네트워크를 만드는 방법을 알아봅니다."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a31f4f12-54ee-4339-b968-1a8097ca77d3
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e7072ddf51570d46578111e2e392e3cbea53f2aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-network-using-powershell"></a><span data-ttu-id="4f3fb-103">PowerShell을 사용하여 가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="4f3fb-103">Create a virtual network using PowerShell</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="4f3fb-104">Azure에는 Azure Resource Manager 및 클래식이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f3fb-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="4f3fb-105">Resource Manager 배포 모델을 통해 리소스를 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4f3fb-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="4f3fb-106">두 가지 모델의 차이점에 대해 자세히 알아보려면 [Azure 배포 모델 이해](../azure-resource-manager/resource-manager-deployment-model.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f3fb-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>
 
<span data-ttu-id="4f3fb-107">이 문서는 PowerShell을 사용하여 Resource Manager 배포 모델을 통해 VNet을 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4f3fb-107">This article explains how to create a VNet through the Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="4f3fb-108">다른 도구를 사용하여 Resource Manager를 통해 VNet을 만들거나 다음 목록에서 다른 옵션을 선택하여 클래식 배포 모델을 통해 VNet을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f3fb-108">You can also create a VNet through Resource Manager using other tools or create a VNet through the classic deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4f3fb-109">포털</span><span class="sxs-lookup"><span data-stu-id="4f3fb-109">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
> * [<span data-ttu-id="4f3fb-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4f3fb-110">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
> * [<span data-ttu-id="4f3fb-111">CLI</span><span class="sxs-lookup"><span data-stu-id="4f3fb-111">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
> * [<span data-ttu-id="4f3fb-112">템플릿</span><span class="sxs-lookup"><span data-stu-id="4f3fb-112">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
> * [<span data-ttu-id="4f3fb-113">포털(클래식)</span><span class="sxs-lookup"><span data-stu-id="4f3fb-113">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
> * [<span data-ttu-id="4f3fb-114">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="4f3fb-114">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [<span data-ttu-id="4f3fb-115">CLI(클래식)</span><span class="sxs-lookup"><span data-stu-id="4f3fb-115">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a><span data-ttu-id="4f3fb-116">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="4f3fb-116">Create a virtual network</span></span>

<span data-ttu-id="4f3fb-117">PowerShell 사용하여 가상 네트워크를 만들려면 다음 단계를 완료하세요.</span><span class="sxs-lookup"><span data-stu-id="4f3fb-117">To create a virtual network using PowerShell, complete the following steps:</span></span>

1. <span data-ttu-id="4f3fb-118">[Azure PowerShell 설치 및 구성](/powershell/azure/overview) 문서에 나오는 단계에 따라 Azure PowerShell을 설치 및 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="4f3fb-118">Install and configure Azure PowerShell, by following the steps in the [How to Install and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>

2. <span data-ttu-id="4f3fb-119">필요에 따라 아래와 같이 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4f3fb-119">If necessary, create a new resource group, as shown below.</span></span> <span data-ttu-id="4f3fb-120">이 시나리오의 경우 이름이 *TestRG*인 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4f3fb-120">For this scenario, create a resource group named *TestRG*.</span></span> <span data-ttu-id="4f3fb-121">리소스 그룹에 대한 자세한 내용은 [Azure 리소스 관리자 개요](../azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f3fb-121">For more information about resource groups, visit [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    ```powershell   
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    <span data-ttu-id="4f3fb-122">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="4f3fb-122">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG    
3. <span data-ttu-id="4f3fb-123">*TestVNet*라는 새 Vnet을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4f3fb-123">Create a new VNet named *TestVNet*:</span></span>

    ```powershell
    New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet `
    -AddressPrefix 192.168.0.0/16 -Location centralus
    ```

    <span data-ttu-id="4f3fb-124">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="4f3fb-124">Expected output:</span></span>

        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                   : W/"[Id]"
        ProvisioningState          : Succeeded
        Tags                       : 
        AddressSpace               : {
                                   "AddressPrefixes": [
                                     "192.168.0.0/16"
                                   ]
                                  }
        DhcpOptions                : {}
        Subnets                    : []
        VirtualNetworkPeerings     : []
4. <span data-ttu-id="4f3fb-125">가상 네트워크 개체를 변수에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="4f3fb-125">Store the virtual network object in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

   > [!TIP]
   > <span data-ttu-id="4f3fb-126">`$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus`을 실행하여 3과 4 단계를 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f3fb-126">You can combine steps 3 and 4 by running `$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus`.</span></span>
   > 

5. <span data-ttu-id="4f3fb-127">새 VNet 변수에 서브넷을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4f3fb-127">Add a subnet to the new VNet variable:</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name FrontEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.1.0/24
    ```

    <span data-ttu-id="4f3fb-128">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="4f3fb-128">Expected output:</span></span>
   
        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                  : W/"[Id]"
        ProvisioningState     : Succeeded
        Tags                  :
        AddressSpace          : {
                                  "AddressPrefixes": [
                                    "192.168.0.0/16"
                                  ]
                                }
        DhcpOptions           : {}
        Subnets             : [
                                  {
                                    "Name": "FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24"
                                  }
                                ]
        VirtualNetworkPeerings     : []

6. <span data-ttu-id="4f3fb-129">만들려는 각 서브넷에 대해 위의 5단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="4f3fb-129">Repeat step 5 above for each subnet you want to create.</span></span> <span data-ttu-id="4f3fb-130">다음 명령은 이 시나리오에 대해 *BackEnd* 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4f3fb-130">The following command creates the *BackEnd* subnet for the scenario:</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name BackEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.2.0/24
    ```

7. <span data-ttu-id="4f3fb-131">서브넷을 만들 수 있지만 현재는 위의 4단계에서 만드는 VNet을 검색하기 위해 사용하는 지역 변수에만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f3fb-131">Although you create subnets, they currently only exist in the local variable used to retrieve the VNet you create in step 4 above.</span></span> <span data-ttu-id="4f3fb-132">Azure에 대한 변경 내용을 저장하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4f3fb-132">To save the changes to Azure, run the following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```
   
    <span data-ttu-id="4f3fb-133">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="4f3fb-133">Expected output:</span></span>
   
        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                  : W/"[Id]"
        ProvisioningState     : Succeeded
        Tags                  :
        AddressSpace          : {
                                  "AddressPrefixes": [
                                    "192.168.0.0/16"
                                  ]
                                }
        DhcpOptions           : {
                                  "DnsServers": []
                                }
        Subnets               : [
                                  {
                                    "Name": "FrontEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24",
                                    "IpConfigurations": [],
                                    "ProvisioningState": "Succeeded"
                                  },
                                  {
                                    "Name": "BackEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                    "AddressPrefix": "192.168.2.0/24",
                                    "IpConfigurations": [],
                                    "ProvisioningState": "Succeeded"
                                  }
                                ]
        VirtualNetworkPeerings : []

## <a name="next-steps"></a><span data-ttu-id="4f3fb-134">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4f3fb-134">Next steps</span></span>

<span data-ttu-id="4f3fb-135">연결 방법 알아보기:</span><span class="sxs-lookup"><span data-stu-id="4f3fb-135">Learn how to connect:</span></span>

- <span data-ttu-id="4f3fb-136">가상 컴퓨터(VM)에서 가상 네트워크 연결은 [Windows VM 만들기](../virtual-machines/virtual-machines-windows-ps-create.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f3fb-136">A virtual machine (VM) to a virtual network by reading the [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md) article.</span></span> <span data-ttu-id="4f3fb-137">해당 문서의 단계에서 VNet 및 서브넷을 만드는 대신 기존 VNet 및 서브넷을 VM에 연결하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f3fb-137">Instead of creating a VNet and subnet in the steps of the articles, you can select an existing VNet and subnet to connect a VM to.</span></span>
- <span data-ttu-id="4f3fb-138">가상 네트워크에서 다른 가상 네트워크 연결은 [VNet 연결](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f3fb-138">The virtual network to other virtual networks by reading the [Connect VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) article.</span></span>
- <span data-ttu-id="4f3fb-139">가상 네트워크에서 온-프레미스 네트워크 연결은 사이트 간 VPN(가상 사설망) 또는 ExpressRoute 회로를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4f3fb-139">The virtual network to an on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="4f3fb-140">자세한 내용은 [사이트 간 VPN을 사용하여 VNet을 온-프레미스 네트워크에 연결](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) 및 [VNet을 ExpressRoute 회선에 연결](../expressroute/expressroute-howto-linkvnet-arm.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f3fb-140">Learn how by reading the [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-arm.md) articles.</span></span>
