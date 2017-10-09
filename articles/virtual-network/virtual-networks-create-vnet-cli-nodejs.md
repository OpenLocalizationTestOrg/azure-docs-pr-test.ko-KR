---
title: "사용 하 여 가상 네트워크 aaaCreate hello Azure CLI 1.0 | Microsoft Docs"
description: "사용 하 여 가상 네트워크 toocreate Azure CLI 1.0 hello 하는 방법에 대해 알아봅니다 | 리소스 관리자입니다."
services: virtual-network
documentationcenter: 
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: jdial
ms.openlocfilehash: f48a8b23a5994164b71c9b51ee8a6810d17f9392
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-hello-azure-cli"></a><span data-ttu-id="6782c-103">Hello Azure CLI를 사용 하 여 가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="6782c-103">Create a virtual network using hello Azure CLI</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="6782c-104">Azure에는 Azure Resource Manager 및 클래식이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6782c-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="6782c-105">Hello 리소스 관리자 배포 모델을 통해 리소스를 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6782c-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="6782c-106">hello 읽기에 대해 더 알아봅니다 toolearn hello 두 모델 간의 차이 hello [이해 Azure 배포 모델](../azure-resource-manager/resource-manager-deployment-model.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="6782c-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="6782c-107">CLI 버전 toocomplete hello 작업</span><span class="sxs-lookup"><span data-stu-id="6782c-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="6782c-108">Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6782c-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="6782c-109">[Azure CLI 2.0](virtual-networks-create-vnet-arm-cli.md) -우리의 차세대 CLI hello 리소스 관리 배포 모델에 대 한</span><span class="sxs-lookup"><span data-stu-id="6782c-109">[Azure CLI 2.0](virtual-networks-create-vnet-arm-cli.md) - our next generation CLI for hello resource management deployment model</span></span>
- <span data-ttu-id="6782c-110">[Azure CLI 1.0](#create-a-virtual-network) – 우리의 CLI 모델에 대 한 hello 클래식 및 리소스 관리 배포 (이 문서)</span><span class="sxs-lookup"><span data-stu-id="6782c-110">[Azure CLI 1.0](#create-a-virtual-network) – our CLI for hello classic and resource management deployment models (this article)</span></span>

 
[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a><span data-ttu-id="6782c-111">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="6782c-111">Create a virtual network</span></span>

<span data-ttu-id="6782c-112">사용 하 여 가상 네트워크 toocreate hello Azure CLI, 단계를 수행 하는 전체 hello:</span><span class="sxs-lookup"><span data-stu-id="6782c-112">toocreate a virtual network using hello Azure CLI, complete hello following steps:</span></span>

1. <span data-ttu-id="6782c-113">에서 설치 및 구성 단계를 다음 hello 하 여 Azure CLI hello hello [설치 및 구성 hello Azure CLI](../cli-install-nodejs.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="6782c-113">Install and configure hello Azure CLI by following hello steps in hello [Install and Configure hello Azure CLI](../cli-install-nodejs.md) article.</span></span>

2. <span data-ttu-id="6782c-114">VNet 및 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6782c-114">Create a VNet and a subnet:</span></span>

    ```azurecli
    azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
    ```

    <span data-ttu-id="6782c-115">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="6782c-115">Expected output:</span></span>
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK

    <span data-ttu-id="6782c-116">사용된 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="6782c-116">Parameters used:</span></span>

   * <span data-ttu-id="6782c-117">**--vnet**.</span><span class="sxs-lookup"><span data-stu-id="6782c-117">**--vnet**.</span></span> <span data-ttu-id="6782c-118">만든 hello VNet toobe의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6782c-118">Name of hello VNet toobe created.</span></span> <span data-ttu-id="6782c-119">이 시나리오에서는 *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="6782c-119">For our scenario, *TestVNet*</span></span>
   * <span data-ttu-id="6782c-120">**-e(또는 --address-space)**.</span><span class="sxs-lookup"><span data-stu-id="6782c-120">**-e (or --address-space)**.</span></span> <span data-ttu-id="6782c-121">VNet 주소 공간입니다.</span><span class="sxs-lookup"><span data-stu-id="6782c-121">VNet address space.</span></span> <span data-ttu-id="6782c-122">이 시나리오에서는 *192.168.0.0*</span><span class="sxs-lookup"><span data-stu-id="6782c-122">For our scenario, *192.168.0.0*</span></span>
   * <span data-ttu-id="6782c-123">**-i(또는 -cidr)**.</span><span class="sxs-lookup"><span data-stu-id="6782c-123">**-i (or -cidr)**.</span></span> <span data-ttu-id="6782c-124">CIDR 형식의 네트워크 마스크입니다.</span><span class="sxs-lookup"><span data-stu-id="6782c-124">Network mask in CIDR format.</span></span> <span data-ttu-id="6782c-125">이 시나리오에서는 *16*입니다.</span><span class="sxs-lookup"><span data-stu-id="6782c-125">For our scenario, *16*.</span></span>
   * <span data-ttu-id="6782c-126">**-n(또는 --subnet-name**).</span><span class="sxs-lookup"><span data-stu-id="6782c-126">**-n (or --subnet-name**).</span></span> <span data-ttu-id="6782c-127">Hello 첫 번째 서브넷의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6782c-127">Name of hello first subnet.</span></span> <span data-ttu-id="6782c-128">이 시나리오에서는 *FrontEnd*입니다.</span><span class="sxs-lookup"><span data-stu-id="6782c-128">For our scenario, *FrontEnd*.</span></span>
   * <span data-ttu-id="6782c-129">**-p(또는 --subnet-start-ip)**.</span><span class="sxs-lookup"><span data-stu-id="6782c-129">**-p (or --subnet-start-ip)**.</span></span> <span data-ttu-id="6782c-130">서브넷 또는 서브넷 주소 공간의 시작 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="6782c-130">Starting IP address for subnet, or subnet address space.</span></span> <span data-ttu-id="6782c-131">이 시나리오에서는 *192.168.1.0*입니다.</span><span class="sxs-lookup"><span data-stu-id="6782c-131">For our scenario, *192.168.1.0*.</span></span>
   * <span data-ttu-id="6782c-132">**-r(또는 --subnet-cidr)**.</span><span class="sxs-lookup"><span data-stu-id="6782c-132">**-r (or --subnet-cidr)**.</span></span> <span data-ttu-id="6782c-133">서브넷에 대한 CIDR 형식의 네트워크 마스크입니다.</span><span class="sxs-lookup"><span data-stu-id="6782c-133">Network mask in CIDR format for subnet.</span></span> <span data-ttu-id="6782c-134">이 시나리오에서는 *24*입니다.</span><span class="sxs-lookup"><span data-stu-id="6782c-134">For our scenario, *24*.</span></span>
   * <span data-ttu-id="6782c-135">**-l(또는 --location)**.</span><span class="sxs-lookup"><span data-stu-id="6782c-135">**-l (or --location)**.</span></span> <span data-ttu-id="6782c-136">Azure 지역 VNet hello 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6782c-136">Azure region where hello VNet is created.</span></span> <span data-ttu-id="6782c-137">이 시나리오에서는 *Central US*입니다.</span><span class="sxs-lookup"><span data-stu-id="6782c-137">For our scenario, *Central US*.</span></span>

3. <span data-ttu-id="6782c-138">서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6782c-138">Create a subnet:</span></span>

    ```azurecli
    azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
    ```
   
    <span data-ttu-id="6782c-139">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="6782c-139">Expected output:</span></span>

            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK

    <span data-ttu-id="6782c-140">사용된 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="6782c-140">Parameters used:</span></span>

   * <span data-ttu-id="6782c-141">**-t(또는 --vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="6782c-141">**-t (or --vnet-name**.</span></span> <span data-ttu-id="6782c-142">Hello hello 서브넷을 만들 수는 VNet의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6782c-142">Name of hello VNet where hello subnet will be created.</span></span> <span data-ttu-id="6782c-143">이 시나리오에서는 *TestVNet*입니다.</span><span class="sxs-lookup"><span data-stu-id="6782c-143">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="6782c-144">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="6782c-144">**-n (or --name)**.</span></span> <span data-ttu-id="6782c-145">Hello 새 서브넷의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6782c-145">Name of hello new subnet.</span></span> <span data-ttu-id="6782c-146">이 시나리오에서는 *BackEnd*입니다.</span><span class="sxs-lookup"><span data-stu-id="6782c-146">For our scenario, *BackEnd*.</span></span>
   * <span data-ttu-id="6782c-147">**-a(또는 --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="6782c-147">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="6782c-148">서브넷 CIDR 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="6782c-148">Subnet CIDR block.</span></span> <span data-ttu-id="6782c-149">이 시나리오에서는 *192.168.2.0/24*입니다.</span><span class="sxs-lookup"><span data-stu-id="6782c-149">Four our scenario, *192.168.2.0/24*.</span></span>
   
4. <span data-ttu-id="6782c-150">tooview hello 속성을 새 VNet을 hello:</span><span class="sxs-lookup"><span data-stu-id="6782c-150">tooview hello properties of hello new VNet:</span></span>

    ```azurecli
    azure network vnet show
    ```
   
    <span data-ttu-id="6782c-151">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="6782c-151">Expected output:</span></span>
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

## <a name="next-steps"></a><span data-ttu-id="6782c-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6782c-152">Next steps</span></span>

<span data-ttu-id="6782c-153">자세한 내용은 방법 tooconnect:</span><span class="sxs-lookup"><span data-stu-id="6782c-153">Learn how tooconnect:</span></span>

- <span data-ttu-id="6782c-154">Hello를 참조 하 여 가상 컴퓨터 (VM) tooa 가상 네트워크 [Linux VM을 만들](../virtual-machines/linux/quick-create-cli.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="6782c-154">A virtual machine (VM) tooa virtual network by reading hello [Create a Linux VM](../virtual-machines/linux/quick-create-cli.md) article.</span></span> <span data-ttu-id="6782c-155">Hello 아티클의 hello 단계에서 VNet 및 서브넷을 만드는 대신 및 선택할 수 있습니다는 기존 VNet 서브넷 tooconnect VM을 합니다.</span><span class="sxs-lookup"><span data-stu-id="6782c-155">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="6782c-156">hello를 참조 하 여 가상 네트워크 tooother 가상 네트워크를 hello [Vnet 연결](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="6782c-156">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) article.</span></span>
- <span data-ttu-id="6782c-157">가상 네트워크 tooan hello 온-프레미스 사이트 간 가상 사설망 (VPN) 또는 express 경로 회로 사용 하 여 네트워크.</span><span class="sxs-lookup"><span data-stu-id="6782c-157">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="6782c-158">자세한 방법은 hello [사이트 간 VPN을 사용 하 여 VNet tooan 온-프레미스 네트워크 연결](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) 및 [VNet tooan ExpressRoute 회로 연결](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6782c-158">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>
