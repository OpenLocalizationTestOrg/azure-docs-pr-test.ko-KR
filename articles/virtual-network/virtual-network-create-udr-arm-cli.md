---
title: "Azure CLI 2.0을 사용하여 라우팅 및 가상 어플라이언스 제어 | Microsoft Docs"
description: "Azure CLI 2.0을 사용하여 라우팅 및 가상 어플라이언스 제어 방법을 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5452a0b8-21a6-4699-8d6a-e2d8faf32c25
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/12/2017
ms.author: jdial
ms.openlocfilehash: e5d9519998346619093f443b740c8904283f76e8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-user-defined-routes-udr-using-the-azure-cli-20"></a><span data-ttu-id="9d32c-103">Azure CLI 2.0을 사용하여 USR(사용자 정의 경로) 만들기</span><span class="sxs-lookup"><span data-stu-id="9d32c-103">Create User-Defined Routes (UDR) using the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9d32c-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9d32c-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="9d32c-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9d32c-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="9d32c-106">템플릿</span><span class="sxs-lookup"><span data-stu-id="9d32c-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="9d32c-107">PowerShell(클래식 배포)</span><span class="sxs-lookup"><span data-stu-id="9d32c-107">PowerShell (Classic deployment)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="9d32c-108">CLI(클래식 배포)</span><span class="sxs-lookup"><span data-stu-id="9d32c-108">CLI (Classic deployment)</span></span>](virtual-network-create-udr-classic-cli.md)

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="9d32c-109">태스크를 완료하기 위한 CLI 버전</span><span class="sxs-lookup"><span data-stu-id="9d32c-109">CLI versions to complete the task</span></span> 

<span data-ttu-id="9d32c-110">다음 CLI 버전 중 하나를 사용하여 태스크를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d32c-110">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="9d32c-111">[Azure CLI 1.0](virtual-network-create-udr-arm-cli-nodejs.md) - 클래식 및 리소스 관리 배포 모델용 CLI</span><span class="sxs-lookup"><span data-stu-id="9d32c-111">[Azure CLI 1.0](virtual-network-create-udr-arm-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span> 
- <span data-ttu-id="9d32c-112">[Azure CLI 2.0](#Create-the-UDR-for-the-front-end-subnet) - 리소스 관리 배포 모델용 차세대 CLI(이 문서)</span><span class="sxs-lookup"><span data-stu-id="9d32c-112">[Azure CLI 2.0](#Create-the-UDR-for-the-front-end-subnet) - our next generation CLI for the resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="9d32c-113">아래 샘플 Azure CLI 명령에는 위의 시나리오를 기반으로 이미 만들어져 있는 단순한 환경이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9d32c-113">The sample Azure CLI commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="9d32c-114">이 문서에 표시된 대로 명령을 실행하려는 경우 먼저 [이 템플릿](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before)을 배포하여 테스트 환경을 구축하고 **Azure에 배포**를 클릭한 다음 필요한 경우 기본 매개 변수 값을 바꾸고 포털의 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="9d32c-114">If you want to run the commands as they are displayed in this document, first build the test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>


## <a name="create-the-udr-for-the-front-end-subnet"></a><span data-ttu-id="9d32c-115">프런트 엔드 서브넷에 대한 UDR 만들기</span><span class="sxs-lookup"><span data-stu-id="9d32c-115">Create the UDR for the front-end subnet</span></span>
<span data-ttu-id="9d32c-116">위의 시나리오에 따라 필요한 경로 테이블 및 경로를 만들려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9d32c-116">To create the route table and route needed for the front end subnet based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="9d32c-117">[az network route-table create](/cli/azure/network/route-table#create) 명령을 사용하여 프런트 엔드 서브넷에 대한 경로 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9d32c-117">Create a route table for the front-end subnet with the [az network route-table create](/cli/azure/network/route-table#create) command:</span></span>

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --location centralus \
    --name UDR-FrontEnd
    ```

    <span data-ttu-id="9d32c-118">출력:</span><span class="sxs-lookup"><span data-stu-id="9d32c-118">Output:</span></span>

    ```json
    {
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd",
    "location": "centralus",
    "name": "UDR-FrontEnd",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "routes": [],
    "subnets": null,
    "tags": null,
    "type": "Microsoft.Network/routeTables"
    }
    ```

2. <span data-ttu-id="9d32c-119">[az network route-table route create](/cli/azure/network/route-table/route#create) 명령을 사용하여 백 엔드 서브넷(192.168.2.0/24)으로 지정된 모든 트래픽을 **FW1** VM(192.168.0.4)으로 전송하는 경로를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9d32c-119">Create a route that sends all traffic destined to the back-end subnet (192.168.2.0/24) to the **FW1** VM (192.168.0.4) using the [az network route-table route create](/cli/azure/network/route-table/route#create) command:</span></span>

    ```azurecli 
    az network route-table route create \
    --resource-group testrg \
    --name RouteToBackEnd \
    --route-table-name UDR-FrontEnd \
    --address-prefix 192.168.2.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

    <span data-ttu-id="9d32c-120">출력:</span><span class="sxs-lookup"><span data-stu-id="9d32c-120">Output:</span></span>

    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd/routes/RouteToBackEnd",
    "name": "RouteToBackEnd",
    "nextHopIpAddress": "192.168.0.4",
    "nextHopType": "VirtualAppliance",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg"
    }
    ```
    <span data-ttu-id="9d32c-121">매개 변수:</span><span class="sxs-lookup"><span data-stu-id="9d32c-121">Parameters:</span></span>

    * <span data-ttu-id="9d32c-122">**--route-table-name**.</span><span class="sxs-lookup"><span data-stu-id="9d32c-122">**--route-table-name**.</span></span> <span data-ttu-id="9d32c-123">경로가 추가될 경로 테이블의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9d32c-123">Name of the route table where the route will be added.</span></span> <span data-ttu-id="9d32c-124">이 시나리오에서는 *UDR-FrontEnd*입니다.</span><span class="sxs-lookup"><span data-stu-id="9d32c-124">For our scenario, *UDR-FrontEnd*.</span></span>
    * <span data-ttu-id="9d32c-125">**--address-prefix**.</span><span class="sxs-lookup"><span data-stu-id="9d32c-125">**--address-prefix**.</span></span> <span data-ttu-id="9d32c-126">패킷을 보내는 서브넷에 대한 주소 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="9d32c-126">Address prefix for the subnet where packets are destined to.</span></span> <span data-ttu-id="9d32c-127">이 시나리오에서는 *192.168.2.0/24*입니다.</span><span class="sxs-lookup"><span data-stu-id="9d32c-127">For our scenario, *192.168.2.0/24*.</span></span>
    * <span data-ttu-id="9d32c-128">**--next-hop-type**.</span><span class="sxs-lookup"><span data-stu-id="9d32c-128">**--next-hop-type**.</span></span> <span data-ttu-id="9d32c-129">전송할 개체 트래픽 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="9d32c-129">Type of object traffic will be sent to.</span></span> <span data-ttu-id="9d32c-130">가능한 값은 *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* 또는 *None*입니다.</span><span class="sxs-lookup"><span data-stu-id="9d32c-130">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
    * <span data-ttu-id="9d32c-131">**--next-hop-ip-address**.</span><span class="sxs-lookup"><span data-stu-id="9d32c-131">**--next-hop-ip-address**.</span></span> <span data-ttu-id="9d32c-132">다음 홉에 대한 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="9d32c-132">IP address for next hop.</span></span> <span data-ttu-id="9d32c-133">이 시나리오에서는 *192.168.0.4*입니다.</span><span class="sxs-lookup"><span data-stu-id="9d32c-133">For our scenario, *192.168.0.4*.</span></span>

3. <span data-ttu-id="9d32c-134">[az network vnet subnet update](/cli/azure/network/vnet/subnet#update) 명령을 실행하여 위에서 만든 경로 테이블을 **FrontEnd** 서브넷에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9d32c-134">Run the [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) command to associate the route table created above with the **FrontEnd** subnet:</span></span>

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name FrontEnd \
    --route-table UDR-FrontEnd
    ```

    <span data-ttu-id="9d32c-135">출력:</span><span class="sxs-lookup"><span data-stu-id="9d32c-135">Output:</span></span>

    ```json
    {
    "addressPrefix": "192.168.1.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testvnet/subnets/FrontEnd",
    "ipConfigurations": null,
    "name": "FrontEnd",
    "networkSecurityGroup": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "resourceNavigationLinks": null,
    "routeTable": {
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd",
        "location": null,
        "name": null,
        "provisioningState": null,
        "resourceGroup": "testrg",
        "routes": null,
        "subnets": null,
        "tags": null,
        "type": null
        }
    }
    ```

    <span data-ttu-id="9d32c-136">매개 변수:</span><span class="sxs-lookup"><span data-stu-id="9d32c-136">Parameters:</span></span>
    
    * <span data-ttu-id="9d32c-137">**--vnet-name**.</span><span class="sxs-lookup"><span data-stu-id="9d32c-137">**--vnet-name**.</span></span> <span data-ttu-id="9d32c-138">서브넷이 위치한 VNet의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9d32c-138">Name of the VNet where the subnet is located.</span></span> <span data-ttu-id="9d32c-139">이 시나리오에서는 *TestVNet*입니다.</span><span class="sxs-lookup"><span data-stu-id="9d32c-139">For our scenario, *TestVNet*.</span></span>

## <a name="create-the-udr-for-the-back-end-subnet"></a><span data-ttu-id="9d32c-140">백 엔드 서브넷에 대한 UDR 만들기</span><span class="sxs-lookup"><span data-stu-id="9d32c-140">Create the UDR for the back-end subnet</span></span>

<span data-ttu-id="9d32c-141">위의 시나리오에 따라 백 엔드 서브넷에 필요한 경로 테이블 및 경로를 만들려면 다음 단계를 마칩니다.</span><span class="sxs-lookup"><span data-stu-id="9d32c-141">To create the route table and route needed for the back-end subnet based on the scenario above, complete the following steps:</span></span>

1. <span data-ttu-id="9d32c-142">다음 명령을 실행하여 백 엔드 서브넷에 대한 경로 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9d32c-142">Run the following command to create a route table for the back-end subnet:</span></span>

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --name UDR-BackEnd \
    --location centralus
    ```

2. <span data-ttu-id="9d32c-143">다음 명령을 실행하여 경로 테이블에 경로를 만들고 프런트 엔드 서브넷(192.168.1.0/24)으로 보내진 모든 트래픽을 **FW1** VM(192.168.0.4)으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9d32c-143">Run the following command to create a route in the route table to send all traffic destined to the front-end subnet (192.168.1.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    az network route-table route create \
    --resource-group testrg \
    --name RouteToFrontEnd \
    --route-table-name UDR-BackEnd \
    --address-prefix 192.168.1.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

3. <span data-ttu-id="9d32c-144">다음 명령을 실행하여 경로 테이블을 **BackEnd** 서브넷에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9d32c-144">Run the following command to associate the route table with the **BackEnd** subnet:</span></span>

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name BackEnd \
    --route-table UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="9d32c-145">FW1에서 IP 전달을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="9d32c-145">Enable IP forwarding on FW1</span></span>

<span data-ttu-id="9d32c-146">사용 되는 NIC에서 IP 전달을 사용 하도록 설정 하려면 **FW1**, 다음 단계를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d32c-146">To enable IP forwarding in the NIC used by **FW1**, complete the following steps:</span></span>

1. <span data-ttu-id="9d32c-147">JMESPATH 필터와 함께 [az network nic show](/cli/azure/network/nic#show) 명령을 실행하여 **IP 전달 사용**에 대한 현재 **enable-ip-forwarding** 값을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9d32c-147">Run the [az network nic show](/cli/azure/network/nic#show) command with a JMESPATH filter to display the current **enable-ip-forwarding** value for **Enable IP forwarding**.</span></span> <span data-ttu-id="9d32c-148">*false*로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d32c-148">It should be set to *false*.</span></span>

    ```azurecli
    az network nic show \
    --resource-group testrg \
    --nname nicfw1 \
    --query 'enableIpForwarding' -o tsv
    ```

    <span data-ttu-id="9d32c-149">출력</span><span class="sxs-lookup"><span data-stu-id="9d32c-149">Output:</span></span>

        false

2. <span data-ttu-id="9d32c-150">다음 명령을 실행하여 IP 전달을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9d32c-150">Run the following command to enable IP forwarding:</span></span>

    ```azurecli
    az network nic update \
    --resource-group testrg \
    --name nicfw1 \
    --ip-forwarding true
    ```

    <span data-ttu-id="9d32c-151">콘솔로 스트리밍되는 출력을 검사하거나 특정 **enableIpForwarding** 값만 다시 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d32c-151">You can examine the output streamed to the console, or just retest for the specific **enableIpForwarding** value:</span></span>

    ```azurecli
    az network nic show -g testrg -n nicfw1 --query 'enableIpForwarding' -o tsv
    ```

    <span data-ttu-id="9d32c-152">출력:</span><span class="sxs-lookup"><span data-stu-id="9d32c-152">Output:</span></span>

        true

    <span data-ttu-id="9d32c-153">매개 변수</span><span class="sxs-lookup"><span data-stu-id="9d32c-153">Parameters:</span></span>

    <span data-ttu-id="9d32c-154">**--ip-forwarding**: *true* 또는 *false*.</span><span class="sxs-lookup"><span data-stu-id="9d32c-154">**--ip-forwarding**: *true* or *false*.</span></span>

