---
title: "aaaControl 라우팅 및 가상 어플라이언스를 사용 하 여 hello Azure CLI 1.0 | Microsoft Docs"
description: "Toocontrol 라우팅 및 가상 어플라이언스를 사용 하 여 Azure CLI 1.0 hello 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 1c8a552d949521fa554880c00405e65fa47a8162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-hello-azure-cli-10"></a><span data-ttu-id="f2970-103">사용자 정의 경로 (UDR) hello Azure CLI 1.0을 사용 하 여 만들기</span><span class="sxs-lookup"><span data-stu-id="f2970-103">Create User-Defined Routes (UDR) using hello Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f2970-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f2970-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="f2970-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f2970-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="f2970-106">템플릿</span><span class="sxs-lookup"><span data-stu-id="f2970-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="f2970-107">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="f2970-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="f2970-108">CLI(클래식)</span><span class="sxs-lookup"><span data-stu-id="f2970-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

<span data-ttu-id="f2970-109">사용자 지정 라우팅 및 가상 어플라이언스 hello Azure CLI를 사용 하 여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f2970-109">Create custom routing and virtual appliances using hello Azure CLI.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="f2970-110">CLI 버전 toocomplete hello 작업</span><span class="sxs-lookup"><span data-stu-id="f2970-110">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="f2970-111">Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2970-111">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="f2970-112">[Azure CLI 1.0](#Create-the-UDR-for-the-front-end-subnet) – 우리의 CLI 모델에 대 한 hello 클래식 및 리소스 관리 배포 (이 문서)</span><span class="sxs-lookup"><span data-stu-id="f2970-112">[Azure CLI 1.0](#Create-the-UDR-for-the-front-end-subnet) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="f2970-113">[Azure CLI 2.0](virtual-network-create-udr-arm-cli.md) -우리의 차세대 CLI hello 리소스 관리 배포 모델에 대 한</span><span class="sxs-lookup"><span data-stu-id="f2970-113">[Azure CLI 2.0](virtual-network-create-udr-arm-cli.md) - our next generation CLI for hello resource management deployment model</span></span> 


[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="f2970-114">hello 샘플 Azure CLI 명령 아래에 이미 위의 hello 시나리오를 기반으로 만들어진 단순 환경이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2970-114">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="f2970-115">이 문서에 표시 된 대로 toorun hello 명령을 원하는 경우 먼저 hello 테스트 환경을 구축 배포 하 여 [이 서식 파일](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), 클릭 **tooAzure 배포**, 대체 hello 기본 매개 변수 값 필요한 경우, 및의 지침에 따라 hello hello 포털 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="f2970-115">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>


## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="f2970-116">Hello UDR hello 프런트 엔드 서브넷에 대 한 만들기</span><span class="sxs-lookup"><span data-stu-id="f2970-116">Create hello UDR for hello front-end subnet</span></span>
<span data-ttu-id="f2970-117">toocreate hello 경로 테이블 및 필요한 위의 hello 시나리오에 따라 hello 프런트 엔드 서브넷에 대 한 경로 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2970-117">toocreate hello route table and route needed for hello front end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="f2970-118">다음 명령은 toocreate hello hello 프런트 엔드 서브넷에 대 한 경로 테이블을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2970-118">Run hello following command toocreate a route table for hello front-end subnet:</span></span>

    ```azurecli
    azure network route-table create -g TestRG -n UDR-FrontEnd -l uswest
    ```
   
    <span data-ttu-id="f2970-119">출력:</span><span class="sxs-lookup"><span data-stu-id="f2970-119">Output:</span></span>
   
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
   
    <span data-ttu-id="f2970-120">매개 변수:</span><span class="sxs-lookup"><span data-stu-id="f2970-120">Parameters:</span></span>
   
   * <span data-ttu-id="f2970-121">**-g (or --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="f2970-121">**-g (or --resource-group)**.</span></span> <span data-ttu-id="f2970-122">Hello UDR 만들어지는 hello 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f2970-122">Name of hello resource group where hello UDR will be created.</span></span> <span data-ttu-id="f2970-123">이 시나리오에서는 *TestRG*입니다.</span><span class="sxs-lookup"><span data-stu-id="f2970-123">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="f2970-124">**-l(또는 --location)**.</span><span class="sxs-lookup"><span data-stu-id="f2970-124">**-l (or --location)**.</span></span> <span data-ttu-id="f2970-125">Hello 새 UDR 만들어지는 azure 지역.</span><span class="sxs-lookup"><span data-stu-id="f2970-125">Azure region where hello new UDR will be created.</span></span> <span data-ttu-id="f2970-126">이 시나리오에서는 *westus*입니다.</span><span class="sxs-lookup"><span data-stu-id="f2970-126">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="f2970-127">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="f2970-127">**-n (or --name)**.</span></span> <span data-ttu-id="f2970-128">Hello에 대 한 이름을 새 UDR 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2970-128">Name for hello new UDR.</span></span> <span data-ttu-id="f2970-129">이 시나리오에서는 *UDR-FrontEnd*입니다.</span><span class="sxs-lookup"><span data-stu-id="f2970-129">For our scenario, *UDR-FrontEnd*.</span></span>
2. <span data-ttu-id="f2970-130">모든 트래픽이 toohello 백 엔드 서브넷 (192.168.2.0/24) toohello 명령 toocreate hello 경로 테이블 toosend에서 경로 따라 hello 실행 **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="f2970-130">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello back-end subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -y VirtualAppliance -p 192.168.0.4
    ```
   
    <span data-ttu-id="f2970-131">출력:</span><span class="sxs-lookup"><span data-stu-id="f2970-131">Output:</span></span>
   
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
   
    <span data-ttu-id="f2970-132">매개 변수</span><span class="sxs-lookup"><span data-stu-id="f2970-132">Parameters:</span></span>
   
   * <span data-ttu-id="f2970-133">**-r(또는 --route-table-name)**.</span><span class="sxs-lookup"><span data-stu-id="f2970-133">**-r (or --route-table-name)**.</span></span> <span data-ttu-id="f2970-134">Hello 경로 추가할 hello 경로 테이블의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f2970-134">Name of hello route table where hello route will be added.</span></span> <span data-ttu-id="f2970-135">이 시나리오에서는 *UDR-FrontEnd*입니다.</span><span class="sxs-lookup"><span data-stu-id="f2970-135">For our scenario, *UDR-FrontEnd*.</span></span>
   * <span data-ttu-id="f2970-136">**-a(또는 --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="f2970-136">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="f2970-137">Hello 서브넷에 패킷을 보내는 위치에 대 한 주소 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="f2970-137">Address prefix for hello subnet where packets are destined to.</span></span> <span data-ttu-id="f2970-138">이 시나리오에서는 *192.168.2.0/24*입니다.</span><span class="sxs-lookup"><span data-stu-id="f2970-138">For our scenario, *192.168.2.0/24*.</span></span>
   * <span data-ttu-id="f2970-139">**-y(또는 --next-hop-type)**.</span><span class="sxs-lookup"><span data-stu-id="f2970-139">**-y (or --next-hop-type)**.</span></span> <span data-ttu-id="f2970-140">전송할 개체 트래픽 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="f2970-140">Type of object traffic will be sent to.</span></span> <span data-ttu-id="f2970-141">가능한 값은 *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* 또는 *None*입니다.</span><span class="sxs-lookup"><span data-stu-id="f2970-141">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
   * <span data-ttu-id="f2970-142">**-p(또는 --next-hop-ip-address**).</span><span class="sxs-lookup"><span data-stu-id="f2970-142">**-p (or --next-hop-ip-address**).</span></span> <span data-ttu-id="f2970-143">다음 홉에 대한 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="f2970-143">IP address for next hop.</span></span> <span data-ttu-id="f2970-144">이 시나리오에서는 *192.168.0.4*입니다.</span><span class="sxs-lookup"><span data-stu-id="f2970-144">For our scenario, *192.168.0.4*.</span></span>
3. <span data-ttu-id="f2970-145">실행된 hello 다음 명령은 hello를 사용 하 여 위에서 만든 tooassociate hello 경로 테이블 **프런트 엔드** 서브넷:</span><span class="sxs-lookup"><span data-stu-id="f2970-145">Run hello following command tooassociate hello route table created above with hello **FrontEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    <span data-ttu-id="f2970-146">출력:</span><span class="sxs-lookup"><span data-stu-id="f2970-146">Output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
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
   
    <span data-ttu-id="f2970-147">매개 변수</span><span class="sxs-lookup"><span data-stu-id="f2970-147">Parameters:</span></span>
   
   * <span data-ttu-id="f2970-148">**-e(또는 --vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="f2970-148">**-e (or --vnet-name)**.</span></span> <span data-ttu-id="f2970-149">Hello hello 서브넷 위치한 VNet의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f2970-149">Name of hello VNet where hello subnet is located.</span></span> <span data-ttu-id="f2970-150">이 시나리오에서는 *TestVNet*입니다.</span><span class="sxs-lookup"><span data-stu-id="f2970-150">For our scenario, *TestVNet*.</span></span>

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="f2970-151">Hello UDR hello 백 엔드 서브넷에 대 한 만들기</span><span class="sxs-lookup"><span data-stu-id="f2970-151">Create hello UDR for hello back-end subnet</span></span>
<span data-ttu-id="f2970-152">toocreate hello 경로 테이블 및 위의 단계를 수행 하는 전체 hello hello 시나리오에 따라 hello 백 엔드 서브넷에 필요한 경로:</span><span class="sxs-lookup"><span data-stu-id="f2970-152">toocreate hello route table and route needed for hello back-end subnet based on hello scenario above, complete hello following steps:</span></span>

1. <span data-ttu-id="f2970-153">다음 명령은 toocreate hello hello 백 엔드 서브넷에 대 한 경로 테이블을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2970-153">Run hello following command toocreate a route table for hello back-end subnet:</span></span>

    ```azurecli
    azure network route-table create -g TestRG -n UDR-BackEnd -l westus
    ```

2. <span data-ttu-id="f2970-154">모든 트래픽이 toohello 프런트 엔드 서브넷 (192.168.1.0/24) toohello 명령 toocreate hello 경로 테이블 toosend에서 경로 따라 hello 실행 **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="f2970-154">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -y VirtualAppliance -p 192.168.0.4
    ```

3. <span data-ttu-id="f2970-155">실행 hello 명령 tooassociate hello 경로 테이블 hello로 다음 **백 엔드** 서브넷:</span><span class="sxs-lookup"><span data-stu-id="f2970-155">Run hello following command tooassociate hello route table with hello **BackEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -r UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="f2970-156">FW1에서 IP 전달을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="f2970-156">Enable IP forwarding on FW1</span></span>
<span data-ttu-id="f2970-157">hello에서 사용 하는 NIC에 IP 전달을 tooenable **FW1**완료, 다음 단계 hello:</span><span class="sxs-lookup"><span data-stu-id="f2970-157">tooenable IP forwarding in hello NIC used by **FW1**, complete hello following steps:</span></span>

1. <span data-ttu-id="f2970-158">뒤에 오는 hello 값에 대 한 hello 명령을 실행 **IP 전달을**합니다.</span><span class="sxs-lookup"><span data-stu-id="f2970-158">Run hello command that follows and notice hello value for **Enable IP forwarding**.</span></span> <span data-ttu-id="f2970-159">너무 설정 해야*false*합니다.</span><span class="sxs-lookup"><span data-stu-id="f2970-159">It should be set too*false*.</span></span>

    ```azurecli
    azure network nic show -g TestRG -n NICFW1
    ```

    <span data-ttu-id="f2970-160">출력:</span><span class="sxs-lookup"><span data-stu-id="f2970-160">Output:</span></span>
   
        info:    Executing command network nic show
        info:    Looking up hello network interface "NICFW1"
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
2. <span data-ttu-id="f2970-161">다음 명령 tooenable IP 전달을 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2970-161">Run hello following command tooenable IP forwarding:</span></span>

    ```azurecli
    azure network nic set -g TestRG -n NICFW1 -f true
    ```
   
    <span data-ttu-id="f2970-162">출력:</span><span class="sxs-lookup"><span data-stu-id="f2970-162">Output:</span></span>
   
        info:    Executing command network nic set
        info:    Looking up hello network interface "NICFW1"
        info:    Updating network interface "NICFW1"
        info:    Looking up hello network interface "NICFW1"
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
   
    <span data-ttu-id="f2970-163">매개 변수</span><span class="sxs-lookup"><span data-stu-id="f2970-163">Parameters:</span></span>
   
   * <span data-ttu-id="f2970-164">**-f(또는 --enable-ip-forwarding)**.</span><span class="sxs-lookup"><span data-stu-id="f2970-164">**-f (or --enable-ip-forwarding)**.</span></span> <span data-ttu-id="f2970-165">*true* 또는 *false*.</span><span class="sxs-lookup"><span data-stu-id="f2970-165">*true* or *false*.</span></span>

