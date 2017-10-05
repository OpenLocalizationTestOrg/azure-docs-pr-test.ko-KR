---
title: "Azure CLI 1.0을 사용하여 라우팅 및 가상 어플라이언스 제어 | Microsoft Docs"
description: "Azure CLI 1.0을 사용하여 라우팅 및 가상 어플라이언스 제어 방법 알아보기"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/18/2017
ms.author: jdial
ms.openlocfilehash: 5f21bc7a4fcd9507ea9d6b2b752a2328a7b834f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-user-defined-routes-udr-using-the-azure-cli-10"></a><span data-ttu-id="150ff-103">Azure CLI 1.0을 사용하여 UDR(사용자 정의 경로) 만들기</span><span class="sxs-lookup"><span data-stu-id="150ff-103">Create User-Defined Routes (UDR) using the Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="150ff-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="150ff-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="150ff-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="150ff-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="150ff-106">템플릿</span><span class="sxs-lookup"><span data-stu-id="150ff-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="150ff-107">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="150ff-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="150ff-108">CLI(클래식)</span><span class="sxs-lookup"><span data-stu-id="150ff-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

<span data-ttu-id="150ff-109">Azure CLI를 사용하여 사용자 지정 라우팅 및 가상 어플라이언스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="150ff-109">Create custom routing and virtual appliances using the Azure CLI.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="150ff-110">태스크를 완료하기 위한 CLI 버전</span><span class="sxs-lookup"><span data-stu-id="150ff-110">CLI versions to complete the task</span></span> 

<span data-ttu-id="150ff-111">다음 CLI 버전 중 하나를 사용하여 태스크를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="150ff-111">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="150ff-112">[Azure CLI 1.0](#Create-the-UDR-for-the-front-end-subnet) - 클래식 및 리소스 관리 배포 모델용 CLI(이 문서)</span><span class="sxs-lookup"><span data-stu-id="150ff-112">[Azure CLI 1.0](#Create-the-UDR-for-the-front-end-subnet) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="150ff-113">[Azure CLI 2.0](virtual-network-create-udr-arm-cli.md) - 리소스 관리 배포 모델용 차세대 CLI</span><span class="sxs-lookup"><span data-stu-id="150ff-113">[Azure CLI 2.0](virtual-network-create-udr-arm-cli.md) - our next generation CLI for the resource management deployment model</span></span> 


[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="150ff-114">아래 샘플 Azure CLI 명령에는 위의 시나리오를 기반으로 이미 만들어져 있는 단순한 환경이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="150ff-114">The sample Azure CLI commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="150ff-115">이 문서에 표시된 대로 명령을 실행하려는 경우 먼저 [이 템플릿](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before)을 배포하여 테스트 환경을 구축하고 **Azure에 배포**를 클릭한 다음 필요한 경우 기본 매개 변수 값을 바꾸고 포털의 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="150ff-115">If you want to run the commands as they are displayed in this document, first build the test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>


## <a name="create-the-udr-for-the-front-end-subnet"></a><span data-ttu-id="150ff-116">프런트 엔드 서브넷에 대한 UDR 만들기</span><span class="sxs-lookup"><span data-stu-id="150ff-116">Create the UDR for the front-end subnet</span></span>
<span data-ttu-id="150ff-117">위의 시나리오에 따라 필요한 경로 테이블 및 경로를 만들려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="150ff-117">To create the route table and route needed for the front end subnet based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="150ff-118">다음 명령을 실행하여 프런트 엔드 서브넷에 대한 경로 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="150ff-118">Run the following command to create a route table for the front-end subnet:</span></span>

    ```azurecli
    azure network route-table create -g TestRG -n UDR-FrontEnd -l uswest
    ```
   
    <span data-ttu-id="150ff-119">출력</span><span class="sxs-lookup"><span data-stu-id="150ff-119">Output:</span></span>
   
        info:    Executing command network route-table create
        info:    Looking up route table "UDR-FrontEnd"
        info:    Creating route table "UDR-FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd
        data:    Name                            : UDR-FrontEnd
        data:    Type                            : Microsoft.Network/routeTables
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        info:    network route-table create command OK
   
    <span data-ttu-id="150ff-120">매개 변수:</span><span class="sxs-lookup"><span data-stu-id="150ff-120">Parameters:</span></span>
   
   * <span data-ttu-id="150ff-121">**-g (or --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="150ff-121">**-g (or --resource-group)**.</span></span> <span data-ttu-id="150ff-122">UDR이 만들어지는 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="150ff-122">Name of the resource group where the UDR will be created.</span></span> <span data-ttu-id="150ff-123">이 시나리오에서는 *TestRG*입니다.</span><span class="sxs-lookup"><span data-stu-id="150ff-123">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="150ff-124">**-l(또는 --location)**.</span><span class="sxs-lookup"><span data-stu-id="150ff-124">**-l (or --location)**.</span></span> <span data-ttu-id="150ff-125">새 UDR을 만들 Azure 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="150ff-125">Azure region where the new UDR will be created.</span></span> <span data-ttu-id="150ff-126">이 시나리오에서는 *westus*입니다.</span><span class="sxs-lookup"><span data-stu-id="150ff-126">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="150ff-127">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="150ff-127">**-n (or --name)**.</span></span> <span data-ttu-id="150ff-128">새 UDR의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="150ff-128">Name for the new UDR.</span></span> <span data-ttu-id="150ff-129">이 시나리오에서는 *UDR-FrontEnd*입니다.</span><span class="sxs-lookup"><span data-stu-id="150ff-129">For our scenario, *UDR-FrontEnd*.</span></span>
2. <span data-ttu-id="150ff-130">다음 명령을 실행하여 경로 테이블에 경로를 만들고 백 엔드 서브넷(192.168.2.0/24)으로 보내진 모든 트래픽을 **FW1** VM(192.168.0.4)으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="150ff-130">Run the following command to create a route in the route table to send all traffic destined to the back-end subnet (192.168.2.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -y VirtualAppliance -p 192.168.0.4
    ```
   
    <span data-ttu-id="150ff-131">출력</span><span class="sxs-lookup"><span data-stu-id="150ff-131">Output:</span></span>
   
        info:    Executing command network route-table route create
        info:    Looking up route "RouteToBackEnd" in route table "UDR-FrontEnd"
        info:    Creating route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    Looking up route "RouteToBackEnd" in route table "UDR-FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd/routes/RouteToBackEnd
        data:    Name                            : RouteToBackEnd
        data:    Provisioning state              : Succeeded
        data:    Next hop type                   : VirtualAppliance
        data:    Next hop IP address             : 192.168.0.4
        data:    Address prefix                  : 192.168.2.0/24
        info:    network route-table route create command OK
   
    <span data-ttu-id="150ff-132">매개 변수</span><span class="sxs-lookup"><span data-stu-id="150ff-132">Parameters:</span></span>
   
   * <span data-ttu-id="150ff-133">**-r(또는 --route-table-name)**.</span><span class="sxs-lookup"><span data-stu-id="150ff-133">**-r (or --route-table-name)**.</span></span> <span data-ttu-id="150ff-134">경로가 추가될 경로 테이블의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="150ff-134">Name of the route table where the route will be added.</span></span> <span data-ttu-id="150ff-135">이 시나리오에서는 *UDR-FrontEnd*입니다.</span><span class="sxs-lookup"><span data-stu-id="150ff-135">For our scenario, *UDR-FrontEnd*.</span></span>
   * <span data-ttu-id="150ff-136">**-a(또는 --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="150ff-136">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="150ff-137">패킷을 보내는 서브넷에 대한 주소 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="150ff-137">Address prefix for the subnet where packets are destined to.</span></span> <span data-ttu-id="150ff-138">이 시나리오에서는 *192.168.2.0/24*입니다.</span><span class="sxs-lookup"><span data-stu-id="150ff-138">For our scenario, *192.168.2.0/24*.</span></span>
   * <span data-ttu-id="150ff-139">**-y(또는 --next-hop-type)**.</span><span class="sxs-lookup"><span data-stu-id="150ff-139">**-y (or --next-hop-type)**.</span></span> <span data-ttu-id="150ff-140">전송할 개체 트래픽 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="150ff-140">Type of object traffic will be sent to.</span></span> <span data-ttu-id="150ff-141">가능한 값은 *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* 또는 *None*입니다.</span><span class="sxs-lookup"><span data-stu-id="150ff-141">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
   * <span data-ttu-id="150ff-142">**-p(또는 --next-hop-ip-address**).</span><span class="sxs-lookup"><span data-stu-id="150ff-142">**-p (or --next-hop-ip-address**).</span></span> <span data-ttu-id="150ff-143">다음 홉에 대한 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="150ff-143">IP address for next hop.</span></span> <span data-ttu-id="150ff-144">이 시나리오에서는 *192.168.0.4*입니다.</span><span class="sxs-lookup"><span data-stu-id="150ff-144">For our scenario, *192.168.0.4*.</span></span>
3. <span data-ttu-id="150ff-145">다음 명령을 실행하여 위에서 만든 경로 테이블을 **FrontEnd** 서브넷에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="150ff-145">Run the following command to associate the route table created above with the **FrontEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    <span data-ttu-id="150ff-146">출력</span><span class="sxs-lookup"><span data-stu-id="150ff-146">Output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up the subnet "FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up the subnet "FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:    Network security group          : [object Object]
        data:    Route Table                     : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd
        data:    IP configurations:
        data:      /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConf
        igurations/ipconfig1
        data:      /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB2/ipConf
        igurations/ipconfig1
        data:    
        info:    network vnet subnet set command OK
   
    <span data-ttu-id="150ff-147">매개 변수</span><span class="sxs-lookup"><span data-stu-id="150ff-147">Parameters:</span></span>
   
   * <span data-ttu-id="150ff-148">**-e(또는 --vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="150ff-148">**-e (or --vnet-name)**.</span></span> <span data-ttu-id="150ff-149">서브넷이 위치한 VNet의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="150ff-149">Name of the VNet where the subnet is located.</span></span> <span data-ttu-id="150ff-150">이 시나리오에서는 *TestVNet*입니다.</span><span class="sxs-lookup"><span data-stu-id="150ff-150">For our scenario, *TestVNet*.</span></span>

## <a name="create-the-udr-for-the-back-end-subnet"></a><span data-ttu-id="150ff-151">백 엔드 서브넷에 대한 UDR 만들기</span><span class="sxs-lookup"><span data-stu-id="150ff-151">Create the UDR for the back-end subnet</span></span>
<span data-ttu-id="150ff-152">위의 시나리오에 따라 백 엔드 서브넷에 필요한 경로 테이블 및 경로를 만들려면 다음 단계를 마칩니다.</span><span class="sxs-lookup"><span data-stu-id="150ff-152">To create the route table and route needed for the back-end subnet based on the scenario above, complete the following steps:</span></span>

1. <span data-ttu-id="150ff-153">다음 명령을 실행하여 백 엔드 서브넷에 대한 경로 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="150ff-153">Run the following command to create a route table for the back-end subnet:</span></span>

    ```azurecli
    azure network route-table create -g TestRG -n UDR-BackEnd -l westus
    ```

2. <span data-ttu-id="150ff-154">다음 명령을 실행하여 경로 테이블에 경로를 만들고 프런트 엔드 서브넷(192.168.1.0/24)으로 보내진 모든 트래픽을 **FW1** VM(192.168.0.4)으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="150ff-154">Run the following command to create a route in the route table to send all traffic destined to the front-end subnet (192.168.1.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -y VirtualAppliance -p 192.168.0.4
    ```

3. <span data-ttu-id="150ff-155">다음 명령을 실행하여 경로 테이블을 **BackEnd** 서브넷에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="150ff-155">Run the following command to associate the route table with the **BackEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -r UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="150ff-156">FW1에서 IP 전달을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="150ff-156">Enable IP forwarding on FW1</span></span>
<span data-ttu-id="150ff-157">사용 되는 NIC에서 IP 전달을 사용 하도록 설정 하려면 **FW1**, 다음 단계를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="150ff-157">To enable IP forwarding in the NIC used by **FW1**, complete the following steps:</span></span>

1. <span data-ttu-id="150ff-158">다음 명령을 실행하고 **IP 전달 사용**에 대한 값을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="150ff-158">Run the command that follows and notice the value for **Enable IP forwarding**.</span></span> <span data-ttu-id="150ff-159">*false*로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="150ff-159">It should be set to *false*.</span></span>

    ```azurecli
    azure network nic show -g TestRG -n NICFW1
    ```

    <span data-ttu-id="150ff-160">출력</span><span class="sxs-lookup"><span data-stu-id="150ff-160">Output:</span></span>
   
        info:    Executing command network nic show
        info:    Looking up the network interface "NICFW1"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        networkInterfaces/NICFW1
        data:    Name                            : NICFW1
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    MAC address                     : 00-0D-3A-30-95-B3
        data:    Enable IP forwarding            : false
        data:    Tags                            : displayName=NetworkInterfaces - DMZ
        data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/
        virtualMachines/FW1
        data:    IP configurations:
        data:      Name                          : ipconfig1
        data:      Provisioning state            : Succeeded
        data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        publicIPAddresses/PIPFW1
        data:      Private IP address            : 192.168.0.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/DMZ
        data:    
        info:    network nic show command OK
2. <span data-ttu-id="150ff-161">다음 명령을 실행하여 IP 전달을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="150ff-161">Run the following command to enable IP forwarding:</span></span>

    ```azurecli
    azure network nic set -g TestRG -n NICFW1 -f true
    ```
   
    <span data-ttu-id="150ff-162">출력</span><span class="sxs-lookup"><span data-stu-id="150ff-162">Output:</span></span>
   
        info:    Executing command network nic set
        info:    Looking up the network interface "NICFW1"
        info:    Updating network interface "NICFW1"
        info:    Looking up the network interface "NICFW1"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        networkInterfaces/NICFW1
        data:    Name                            : NICFW1
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    MAC address                     : 00-0D-3A-30-95-B3
        data:    Enable IP forwarding            : true
        data:    Tags                            : displayName=NetworkInterfaces - DMZ
        data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/
        virtualMachines/FW1
        data:    IP configurations:
        data:      Name                          : ipconfig1
        data:      Provisioning state            : Succeeded
        data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        publicIPAddresses/PIPFW1
        data:      Private IP address            : 192.168.0.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/DMZ
        data:    
        info:    network nic set command OK
   
    <span data-ttu-id="150ff-163">매개 변수</span><span class="sxs-lookup"><span data-stu-id="150ff-163">Parameters:</span></span>
   
   * <span data-ttu-id="150ff-164">**-f(또는 --enable-ip-forwarding)**.</span><span class="sxs-lookup"><span data-stu-id="150ff-164">**-f (or --enable-ip-forwarding)**.</span></span> <span data-ttu-id="150ff-165">*true* 또는 *false*.</span><span class="sxs-lookup"><span data-stu-id="150ff-165">*true* or *false*.</span></span>

