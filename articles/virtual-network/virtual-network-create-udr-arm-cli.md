---
title: "aaaControl 라우팅 및 가상 어플라이언스를 사용 하 여 hello Azure CLI 2.0 | Microsoft Docs"
description: "Toocontrol 라우팅 및 가상 어플라이언스를 사용 하 여 Azure CLI 2.0 hello 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 79b908848932a4365dab1b7497b6a0dbf44bbaf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-hello-azure-cli-20"></a><span data-ttu-id="d8b5d-103">사용자 정의 경로 (UDR) hello Azure CLI 2.0을 사용 하 여 만들기</span><span class="sxs-lookup"><span data-stu-id="d8b5d-103">Create User-Defined Routes (UDR) using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d8b5d-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d8b5d-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="d8b5d-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d8b5d-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="d8b5d-106">템플릿</span><span class="sxs-lookup"><span data-stu-id="d8b5d-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="d8b5d-107">PowerShell(클래식 배포)</span><span class="sxs-lookup"><span data-stu-id="d8b5d-107">PowerShell (Classic deployment)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="d8b5d-108">CLI(클래식 배포)</span><span class="sxs-lookup"><span data-stu-id="d8b5d-108">CLI (Classic deployment)</span></span>](virtual-network-create-udr-classic-cli.md)

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="d8b5d-109">CLI 버전 toocomplete hello 작업</span><span class="sxs-lookup"><span data-stu-id="d8b5d-109">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="d8b5d-110">Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8b5d-110">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="d8b5d-111">[Azure CLI 1.0](virtual-network-create-udr-arm-cli-nodejs.md) – hello 클래식 및 리소스 관리 배포 모델에 대 한 우리의 CLI</span><span class="sxs-lookup"><span data-stu-id="d8b5d-111">[Azure CLI 1.0](virtual-network-create-udr-arm-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="d8b5d-112">[Azure CLI 2.0](#Create-the-UDR-for-the-front-end-subnet) -우리의 차세대 CLI hello 리소스 관리 배포 모델 (이 문서)</span><span class="sxs-lookup"><span data-stu-id="d8b5d-112">[Azure CLI 2.0](#Create-the-UDR-for-the-front-end-subnet) - our next generation CLI for hello resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="d8b5d-113">hello 샘플 Azure CLI 명령 아래에 이미 위의 hello 시나리오를 기반으로 만들어진 단순 환경이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b5d-113">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="d8b5d-114">이 문서에 표시 된 대로 toorun hello 명령을 원하는 경우 먼저 hello 테스트 환경을 구축 배포 하 여 [이 서식 파일](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), 클릭 **tooAzure 배포**, 대체 hello 기본 매개 변수 값 필요한 경우, 및의 지침에 따라 hello hello 포털 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="d8b5d-114">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>


## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="d8b5d-115">Hello UDR hello 프런트 엔드 서브넷에 대 한 만들기</span><span class="sxs-lookup"><span data-stu-id="d8b5d-115">Create hello UDR for hello front-end subnet</span></span>
<span data-ttu-id="d8b5d-116">toocreate hello 경로 테이블 및 필요한 위의 hello 시나리오에 따라 hello 프런트 엔드 서브넷에 대 한 경로 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b5d-116">toocreate hello route table and route needed for hello front end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="d8b5d-117">Hello로 hello 프런트 엔드 서브넷에 대 한 경로 테이블 만들기 [az 네트워크 경로 테이블 만들기](/cli/azure/network/route-table#create) 명령:</span><span class="sxs-lookup"><span data-stu-id="d8b5d-117">Create a route table for hello front-end subnet with hello [az network route-table create](/cli/azure/network/route-table#create) command:</span></span>

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --location centralus \
    --name UDR-FrontEnd
    ```

    <span data-ttu-id="d8b5d-118">출력:</span><span class="sxs-lookup"><span data-stu-id="d8b5d-118">Output:</span></span>

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

2. <span data-ttu-id="d8b5d-119">모든 트래픽이 toohello 백 엔드 서브넷 (192.168.2.0/24) toohello 보내는 경로 만들어 **FW1** hello를 사용 하 여 VM (192.168.0.4) [az 네트워크 경로 테이블 경로 만들기](/cli/azure/network/route-table/route#create) 명령:</span><span class="sxs-lookup"><span data-stu-id="d8b5d-119">Create a route that sends all traffic destined toohello back-end subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4) using hello [az network route-table route create](/cli/azure/network/route-table/route#create) command:</span></span>

    ```azurecli 
    az network route-table route create \
    --resource-group testrg \
    --name RouteToBackEnd \
    --route-table-name UDR-FrontEnd \
    --address-prefix 192.168.2.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

    <span data-ttu-id="d8b5d-120">출력:</span><span class="sxs-lookup"><span data-stu-id="d8b5d-120">Output:</span></span>

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
    <span data-ttu-id="d8b5d-121">매개 변수:</span><span class="sxs-lookup"><span data-stu-id="d8b5d-121">Parameters:</span></span>

    * <span data-ttu-id="d8b5d-122">**--route-table-name**.</span><span class="sxs-lookup"><span data-stu-id="d8b5d-122">**--route-table-name**.</span></span> <span data-ttu-id="d8b5d-123">Hello 경로 추가할 hello 경로 테이블의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d8b5d-123">Name of hello route table where hello route will be added.</span></span> <span data-ttu-id="d8b5d-124">이 시나리오에서는 *UDR-FrontEnd*입니다.</span><span class="sxs-lookup"><span data-stu-id="d8b5d-124">For our scenario, *UDR-FrontEnd*.</span></span>
    * <span data-ttu-id="d8b5d-125">**--address-prefix**.</span><span class="sxs-lookup"><span data-stu-id="d8b5d-125">**--address-prefix**.</span></span> <span data-ttu-id="d8b5d-126">Hello 서브넷에 패킷을 보내는 위치에 대 한 주소 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="d8b5d-126">Address prefix for hello subnet where packets are destined to.</span></span> <span data-ttu-id="d8b5d-127">이 시나리오에서는 *192.168.2.0/24*입니다.</span><span class="sxs-lookup"><span data-stu-id="d8b5d-127">For our scenario, *192.168.2.0/24*.</span></span>
    * <span data-ttu-id="d8b5d-128">**--next-hop-type**.</span><span class="sxs-lookup"><span data-stu-id="d8b5d-128">**--next-hop-type**.</span></span> <span data-ttu-id="d8b5d-129">전송할 개체 트래픽 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="d8b5d-129">Type of object traffic will be sent to.</span></span> <span data-ttu-id="d8b5d-130">가능한 값은 *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* 또는 *None*입니다.</span><span class="sxs-lookup"><span data-stu-id="d8b5d-130">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
    * <span data-ttu-id="d8b5d-131">**--next-hop-ip-address**.</span><span class="sxs-lookup"><span data-stu-id="d8b5d-131">**--next-hop-ip-address**.</span></span> <span data-ttu-id="d8b5d-132">다음 홉에 대한 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="d8b5d-132">IP address for next hop.</span></span> <span data-ttu-id="d8b5d-133">이 시나리오에서는 *192.168.0.4*입니다.</span><span class="sxs-lookup"><span data-stu-id="d8b5d-133">For our scenario, *192.168.0.4*.</span></span>

3. <span data-ttu-id="d8b5d-134">Hello 실행 [az 네트워크 vnet 서브넷 업데이트](/cli/azure/network/vnet/subnet#update) 명령 tooassociate hello 경로 테이블 hello로 위에서 만든 **프런트 엔드** 서브넷:</span><span class="sxs-lookup"><span data-stu-id="d8b5d-134">Run hello [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) command tooassociate hello route table created above with hello **FrontEnd** subnet:</span></span>

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name FrontEnd \
    --route-table UDR-FrontEnd
    ```

    <span data-ttu-id="d8b5d-135">출력:</span><span class="sxs-lookup"><span data-stu-id="d8b5d-135">Output:</span></span>

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

    <span data-ttu-id="d8b5d-136">매개 변수:</span><span class="sxs-lookup"><span data-stu-id="d8b5d-136">Parameters:</span></span>
    
    * <span data-ttu-id="d8b5d-137">**--vnet-name**.</span><span class="sxs-lookup"><span data-stu-id="d8b5d-137">**--vnet-name**.</span></span> <span data-ttu-id="d8b5d-138">Hello hello 서브넷 위치한 VNet의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d8b5d-138">Name of hello VNet where hello subnet is located.</span></span> <span data-ttu-id="d8b5d-139">이 시나리오에서는 *TestVNet*입니다.</span><span class="sxs-lookup"><span data-stu-id="d8b5d-139">For our scenario, *TestVNet*.</span></span>

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="d8b5d-140">Hello UDR hello 백 엔드 서브넷에 대 한 만들기</span><span class="sxs-lookup"><span data-stu-id="d8b5d-140">Create hello UDR for hello back-end subnet</span></span>

<span data-ttu-id="d8b5d-141">toocreate hello 경로 테이블 및 위의 단계를 수행 하는 전체 hello hello 시나리오에 따라 hello 백 엔드 서브넷에 필요한 경로:</span><span class="sxs-lookup"><span data-stu-id="d8b5d-141">toocreate hello route table and route needed for hello back-end subnet based on hello scenario above, complete hello following steps:</span></span>

1. <span data-ttu-id="d8b5d-142">다음 명령은 toocreate hello hello 백 엔드 서브넷에 대 한 경로 테이블을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b5d-142">Run hello following command toocreate a route table for hello back-end subnet:</span></span>

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --name UDR-BackEnd \
    --location centralus
    ```

2. <span data-ttu-id="d8b5d-143">모든 트래픽이 toohello 프런트 엔드 서브넷 (192.168.1.0/24) toohello 명령 toocreate hello 경로 테이블 toosend에서 경로 따라 hello 실행 **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="d8b5d-143">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    az network route-table route create \
    --resource-group testrg \
    --name RouteToFrontEnd \
    --route-table-name UDR-BackEnd \
    --address-prefix 192.168.1.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

3. <span data-ttu-id="d8b5d-144">실행 hello 명령 tooassociate hello 경로 테이블 hello로 다음 **백 엔드** 서브넷:</span><span class="sxs-lookup"><span data-stu-id="d8b5d-144">Run hello following command tooassociate hello route table with hello **BackEnd** subnet:</span></span>

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name BackEnd \
    --route-table UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="d8b5d-145">FW1에서 IP 전달을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="d8b5d-145">Enable IP forwarding on FW1</span></span>

<span data-ttu-id="d8b5d-146">hello에서 사용 하는 NIC에 IP 전달을 tooenable **FW1**완료, 다음 단계 hello:</span><span class="sxs-lookup"><span data-stu-id="d8b5d-146">tooenable IP forwarding in hello NIC used by **FW1**, complete hello following steps:</span></span>

1. <span data-ttu-id="d8b5d-147">Hello 실행 [az 네트워크 nic 표시](/cli/azure/network/nic#show) JMESPATH 필터 toodisplay hello 현재 명령을 **사용 ip 전달을** 값에 대 한 **IP 전달을**합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b5d-147">Run hello [az network nic show](/cli/azure/network/nic#show) command with a JMESPATH filter toodisplay hello current **enable-ip-forwarding** value for **Enable IP forwarding**.</span></span> <span data-ttu-id="d8b5d-148">너무 설정 해야*false*합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b5d-148">It should be set too*false*.</span></span>

    ```azurecli
    az network nic show \
    --resource-group testrg \
    --nname nicfw1 \
    --query 'enableIpForwarding' -o tsv
    ```

    <span data-ttu-id="d8b5d-149">출력:</span><span class="sxs-lookup"><span data-stu-id="d8b5d-149">Output:</span></span>

        false

2. <span data-ttu-id="d8b5d-150">다음 명령 tooenable IP 전달을 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8b5d-150">Run hello following command tooenable IP forwarding:</span></span>

    ```azurecli
    az network nic update \
    --resource-group testrg \
    --name nicfw1 \
    --ip-forwarding true
    ```

    <span data-ttu-id="d8b5d-151">Hello 출력 스트리밍된 toohello 콘솔 조사 하거나 특정 hello에 대 한 바로 다시 테스트 하면 **enableIpForwarding** 값:</span><span class="sxs-lookup"><span data-stu-id="d8b5d-151">You can examine hello output streamed toohello console, or just retest for hello specific **enableIpForwarding** value:</span></span>

    ```azurecli
    az network nic show -g testrg -n nicfw1 --query 'enableIpForwarding' -o tsv
    ```

    <span data-ttu-id="d8b5d-152">출력:</span><span class="sxs-lookup"><span data-stu-id="d8b5d-152">Output:</span></span>

        true

    <span data-ttu-id="d8b5d-153">매개 변수</span><span class="sxs-lookup"><span data-stu-id="d8b5d-153">Parameters:</span></span>

    <span data-ttu-id="d8b5d-154">**--ip-forwarding**: *true* 또는 *false*.</span><span class="sxs-lookup"><span data-stu-id="d8b5d-154">**--ip-forwarding**: *true* or *false*.</span></span>

