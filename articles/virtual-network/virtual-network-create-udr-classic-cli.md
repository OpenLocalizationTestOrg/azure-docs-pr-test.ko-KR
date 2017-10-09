---
title: "Azure 가상 네트워크-CLI-클래식에서 aaaControl 라우팅을 | Microsoft Docs"
description: "사용 하 여 Vnet에 라우팅 toocontrol Azure CLI hello 클래식 배포 모델에서 hello 하는 방법에 대해 알아봅니다"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: ca2b4638-8777-4d30-b972-eb790a7c804f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: 07dde573f1a605bf280156c261d51e213ede0cdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-hello-azure-cli"></a><span data-ttu-id="17981-103">컨트롤에서 라우팅 및 사용 하 여 가상 어플라이언스 (클래식)를 사용 하 여 hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="17981-103">Control routing and use virtual appliances (classic) using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="17981-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="17981-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="17981-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="17981-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="17981-106">템플릿</span><span class="sxs-lookup"><span data-stu-id="17981-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="17981-107">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="17981-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="17981-108">CLI(클래식)</span><span class="sxs-lookup"><span data-stu-id="17981-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="17981-109">이 문서에서는 hello 클래식 배포 모델에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="17981-109">This article covers hello classic deployment model.</span></span> <span data-ttu-id="17981-110">수도 있습니다 [라우팅을 제어 하 고 가상 어플라이언스를 사용 하 여 hello 리소스 관리자 배포 모델에서](virtual-network-create-udr-arm-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="17981-110">You can also [control routing and use virtual appliances in hello Resource Manager deployment model](virtual-network-create-udr-arm-cli.md).</span></span>

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="17981-111">hello 샘플 Azure CLI 명령 아래에 이미 위의 hello 시나리오를 기반으로 만들어진 단순 환경이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="17981-111">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="17981-112">이 문서에 표시 된 대로 toorun hello 명령을 하려는 경우 만들 hello 환경에 표시 된 [hello Azure CLI를 사용 하 여 VNet (클래식)을 만들](virtual-networks-create-vnet-classic-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="17981-112">If you want toorun hello commands as they are displayed in this document, create hello environment shown in [create a VNet (classic) using hello Azure CLI](virtual-networks-create-vnet-classic-cli.md).</span></span>

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="17981-113">Hello UDR hello 프런트 엔드 서브넷에 대 한 만들기</span><span class="sxs-lookup"><span data-stu-id="17981-113">Create hello UDR for hello front end subnet</span></span>
<span data-ttu-id="17981-114">toocreate hello 경로 테이블 및 필요한 위의 hello 시나리오에 따라 hello 프런트 엔드 서브넷에 대 한 경로 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="17981-114">toocreate hello route table and route needed for hello front end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="17981-115">다음 명령 tooswitch tooclassic 모드 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="17981-115">Run hello following command tooswitch tooclassic mode:</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="17981-116">출력:</span><span class="sxs-lookup"><span data-stu-id="17981-116">Output:</span></span>

        info:    New mode is asm

2. <span data-ttu-id="17981-117">다음 명령은 toocreate hello hello 프런트 엔드 서브넷에 대 한 경로 테이블을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="17981-117">Run hello following command toocreate a route table for hello front-end subnet:</span></span>

    ```azurecli
    azure network route-table create -n UDR-FrontEnd -l uswest
    ```
   
    <span data-ttu-id="17981-118">출력:</span><span class="sxs-lookup"><span data-stu-id="17981-118">Output:</span></span>
   
        info:    Executing command network route-table create
        info:    Creating route table "UDR-FrontEnd"
        info:    Getting route table "UDR-FrontEnd"
        data:    Name                            : UDR-FrontEnd
        data:    Location                        : West US
        info:    network route-table create command OK
   
    <span data-ttu-id="17981-119">매개 변수</span><span class="sxs-lookup"><span data-stu-id="17981-119">Parameters:</span></span>
   
   * <span data-ttu-id="17981-120">**-l(또는 --location)**.</span><span class="sxs-lookup"><span data-stu-id="17981-120">**-l (or --location)**.</span></span> <span data-ttu-id="17981-121">Azure 지역 hello 새 NSG를 만들 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="17981-121">Azure region where hello new NSG will be created.</span></span> <span data-ttu-id="17981-122">이 시나리오에서는 *westus*입니다.</span><span class="sxs-lookup"><span data-stu-id="17981-122">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="17981-123">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="17981-123">**-n (or --name)**.</span></span> <span data-ttu-id="17981-124">Hello에 대 한 이름을 새 NSG 합니다.</span><span class="sxs-lookup"><span data-stu-id="17981-124">Name for hello new NSG.</span></span> <span data-ttu-id="17981-125">이 시나리오에서는 *NSG-FrontEnd*입니다.</span><span class="sxs-lookup"><span data-stu-id="17981-125">For our scenario, *NSG-FrontEnd*.</span></span>
3. <span data-ttu-id="17981-126">모든 트래픽이 toohello 백 엔드 서브넷 (192.168.2.0/24) toohello 명령 toocreate hello 경로 테이블 toosend에서 경로 따라 hello 실행 **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="17981-126">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello back-end subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route set -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

    <span data-ttu-id="17981-127">출력:</span><span class="sxs-lookup"><span data-stu-id="17981-127">Output:</span></span>
   
        info:    Executing command network route-table route set
        info:    Getting route table "UDR-FrontEnd"
        info:    Setting route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    network route-table route set command OK
   
    <span data-ttu-id="17981-128">매개 변수</span><span class="sxs-lookup"><span data-stu-id="17981-128">Parameters:</span></span>
   
   * <span data-ttu-id="17981-129">**-r(또는 --route-table-name)**.</span><span class="sxs-lookup"><span data-stu-id="17981-129">**-r (or --route-table-name)**.</span></span> <span data-ttu-id="17981-130">Hello 경로 추가할 hello 경로 테이블의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="17981-130">Name of hello route table where hello route will be added.</span></span> <span data-ttu-id="17981-131">이 시나리오에서는 *UDR-FrontEnd*입니다.</span><span class="sxs-lookup"><span data-stu-id="17981-131">For our scenario, *UDR-FrontEnd*.</span></span>
   * <span data-ttu-id="17981-132">**-a(또는 --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="17981-132">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="17981-133">Hello 서브넷에 패킷을 보내는 위치에 대 한 주소 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="17981-133">Address prefix for hello subnet where packets are destined to.</span></span> <span data-ttu-id="17981-134">이 시나리오에서는 *192.168.2.0/24*입니다.</span><span class="sxs-lookup"><span data-stu-id="17981-134">For our scenario, *192.168.2.0/24*.</span></span>
   * <span data-ttu-id="17981-135">**-t(또는 --next-hop-type)**.</span><span class="sxs-lookup"><span data-stu-id="17981-135">**-t (or --next-hop-type)**.</span></span> <span data-ttu-id="17981-136">전송할 개체 트래픽 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="17981-136">Type of object traffic will be sent to.</span></span> <span data-ttu-id="17981-137">가능한 값은 *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* 또는 *None*입니다.</span><span class="sxs-lookup"><span data-stu-id="17981-137">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
   * <span data-ttu-id="17981-138">**-p(또는 --next-hop-ip-address**).</span><span class="sxs-lookup"><span data-stu-id="17981-138">**-p (or --next-hop-ip-address**).</span></span> <span data-ttu-id="17981-139">다음 홉에 대한 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="17981-139">IP address for next hop.</span></span> <span data-ttu-id="17981-140">이 시나리오에서는 *192.168.0.4*입니다.</span><span class="sxs-lookup"><span data-stu-id="17981-140">For our scenario, *192.168.0.4*.</span></span>
4. <span data-ttu-id="17981-141">실행된 hello 다음 명령은 hello를 사용 하 여 만든 tooassociate hello 경로 테이블 **프런트 엔드** 서브넷:</span><span class="sxs-lookup"><span data-stu-id="17981-141">Run hello following command tooassociate hello route table created with hello **FrontEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    <span data-ttu-id="17981-142">출력:</span><span class="sxs-lookup"><span data-stu-id="17981-142">Output:</span></span>
   
        info:    Executing command network vnet subnet route-table add
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        info:    Associating route table "UDR-FrontEnd" and subnet "FrontEnd"
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        data:    Route table name                : UDR-FrontEnd
        data:      Location                      : West US
        data:      Routes:
        info:    network vnet subnet route-table add command OK    
   
    <span data-ttu-id="17981-143">매개 변수</span><span class="sxs-lookup"><span data-stu-id="17981-143">Parameters:</span></span>
   
   * <span data-ttu-id="17981-144">**-t(또는 --vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="17981-144">**-t (or --vnet-name)**.</span></span> <span data-ttu-id="17981-145">Hello hello 서브넷 위치한 VNet의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="17981-145">Name of hello VNet where hello subnet is located.</span></span> <span data-ttu-id="17981-146">이 시나리오에서는 *TestVNet*입니다.</span><span class="sxs-lookup"><span data-stu-id="17981-146">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="17981-147">**-n(또는 --subnet-name**).</span><span class="sxs-lookup"><span data-stu-id="17981-147">**-n (or --subnet-name**.</span></span> <span data-ttu-id="17981-148">Hello 서브넷 hello 경로 테이블의 이름에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17981-148">Name of hello subnet hello route table will be added to.</span></span> <span data-ttu-id="17981-149">이 시나리오에서는 *FrontEnd*입니다.</span><span class="sxs-lookup"><span data-stu-id="17981-149">For our scenario, *FrontEnd*.</span></span>

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="17981-150">Hello UDR hello 백 엔드 서브넷에 대 한 만들기</span><span class="sxs-lookup"><span data-stu-id="17981-150">Create hello UDR for hello back-end subnet</span></span>
<span data-ttu-id="17981-151">toocreate hello 경로 테이블 및 hello 시나리오에서는 다음 단계 완료 hello에 따라 hello 백 엔드 서브넷에 필요한 경로:</span><span class="sxs-lookup"><span data-stu-id="17981-151">toocreate hello route table and route needed for hello back-end subnet based on hello scenario, complete hello following steps:</span></span>

1. <span data-ttu-id="17981-152">다음 명령은 toocreate hello hello 백 엔드 서브넷에 대 한 경로 테이블을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="17981-152">Run hello following command toocreate a route table for hello back-end subnet:</span></span>

    ```azurecli
    azure network route-table create -n UDR-BackEnd -l uswest
    ```

2. <span data-ttu-id="17981-153">모든 트래픽이 toohello 프런트 엔드 서브넷 (192.168.1.0/24) toohello 명령 toocreate hello 경로 테이블 toosend에서 경로 따라 hello 실행 **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="17981-153">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route set -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

3. <span data-ttu-id="17981-154">실행 hello 명령 tooassociate hello 경로 테이블 hello로 다음 **백 엔드** 서브넷:</span><span class="sxs-lookup"><span data-stu-id="17981-154">Run hello following command tooassociate hello route table with hello **BackEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n BackEnd -r UDR-BackEnd
    ```

