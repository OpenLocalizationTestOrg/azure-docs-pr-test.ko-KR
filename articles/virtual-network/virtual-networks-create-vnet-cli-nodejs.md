---
title: "Azure CLI 1.0을 사용하여 가상 네트워크 만들기 | Microsoft Docs"
description: "Azure CLI 1.0을 사용하여 가상 네트워크를 만드는 방법 알아보기 | Resource Manager."
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
ms.openlocfilehash: f0649c5c8c04dda72d2f147601efb37217f9bade
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-network-using-the-azure-cli"></a><span data-ttu-id="8667d-103">Azure CLI를 사용하여 가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="8667d-103">Create a virtual network using the Azure CLI</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="8667d-104">Azure에는 Azure Resource Manager 및 클래식이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8667d-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="8667d-105">Resource Manager 배포 모델을 통해 리소스를 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8667d-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="8667d-106">두 가지 모델의 차이점에 대해 자세히 알아보려면 [Azure 배포 모델 이해](../azure-resource-manager/resource-manager-deployment-model.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8667d-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="8667d-107">태스크를 완료하기 위한 CLI 버전</span><span class="sxs-lookup"><span data-stu-id="8667d-107">CLI versions to complete the task</span></span>
<span data-ttu-id="8667d-108">다음 CLI 버전 중 하나를 사용하여 태스크를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8667d-108">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="8667d-109">[Azure CLI 2.0](virtual-networks-create-vnet-arm-cli.md) - 리소스 관리 배포 모델용 차세대 CLI</span><span class="sxs-lookup"><span data-stu-id="8667d-109">[Azure CLI 2.0](virtual-networks-create-vnet-arm-cli.md) - our next generation CLI for the resource management deployment model</span></span>
- <span data-ttu-id="8667d-110">[Azure CLI 1.0](#create-a-virtual-network) - 클래식 및 리소스 관리 배포 모델용 CLI(이 문서)</span><span class="sxs-lookup"><span data-stu-id="8667d-110">[Azure CLI 1.0](#create-a-virtual-network) – our CLI for the classic and resource management deployment models (this article)</span></span>

 
[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a><span data-ttu-id="8667d-111">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="8667d-111">Create a virtual network</span></span>

<span data-ttu-id="8667d-112">Azure CLI를 사용하여 가상 네트워크를 만들려면 다음 단계를 완료하세요.</span><span class="sxs-lookup"><span data-stu-id="8667d-112">To create a virtual network using the Azure CLI, complete the following steps:</span></span>

1. <span data-ttu-id="8667d-113">[Azure CLI 설치 및 구성](../cli-install-nodejs.md) 문서에 나오는 단계에 따라 Azure CLI를 설치 및 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8667d-113">Install and configure the Azure CLI by following the steps in the [Install and Configure the Azure CLI](../cli-install-nodejs.md) article.</span></span>

2. <span data-ttu-id="8667d-114">VNet 및 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8667d-114">Create a VNet and a subnet:</span></span>

    ```azurecli
    azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
    ```

    <span data-ttu-id="8667d-115">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="8667d-115">Expected output:</span></span>
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK

    <span data-ttu-id="8667d-116">사용된 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="8667d-116">Parameters used:</span></span>

   * <span data-ttu-id="8667d-117">**--vnet**.</span><span class="sxs-lookup"><span data-stu-id="8667d-117">**--vnet**.</span></span> <span data-ttu-id="8667d-118">만들 VNet의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="8667d-118">Name of the VNet to be created.</span></span> <span data-ttu-id="8667d-119">이 시나리오에서는 *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="8667d-119">For our scenario, *TestVNet*</span></span>
   * <span data-ttu-id="8667d-120">**-e(또는 --address-space)**.</span><span class="sxs-lookup"><span data-stu-id="8667d-120">**-e (or --address-space)**.</span></span> <span data-ttu-id="8667d-121">VNet 주소 공간입니다.</span><span class="sxs-lookup"><span data-stu-id="8667d-121">VNet address space.</span></span> <span data-ttu-id="8667d-122">이 시나리오에서는 *192.168.0.0*</span><span class="sxs-lookup"><span data-stu-id="8667d-122">For our scenario, *192.168.0.0*</span></span>
   * <span data-ttu-id="8667d-123">**-i(또는 -cidr)**.</span><span class="sxs-lookup"><span data-stu-id="8667d-123">**-i (or -cidr)**.</span></span> <span data-ttu-id="8667d-124">CIDR 형식의 네트워크 마스크입니다.</span><span class="sxs-lookup"><span data-stu-id="8667d-124">Network mask in CIDR format.</span></span> <span data-ttu-id="8667d-125">이 시나리오에서는 *16*입니다.</span><span class="sxs-lookup"><span data-stu-id="8667d-125">For our scenario, *16*.</span></span>
   * <span data-ttu-id="8667d-126">**-n(또는 --subnet-name**).</span><span class="sxs-lookup"><span data-stu-id="8667d-126">**-n (or --subnet-name**).</span></span> <span data-ttu-id="8667d-127">첫 번째 서브넷의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="8667d-127">Name of the first subnet.</span></span> <span data-ttu-id="8667d-128">이 시나리오에서는 *FrontEnd*입니다.</span><span class="sxs-lookup"><span data-stu-id="8667d-128">For our scenario, *FrontEnd*.</span></span>
   * <span data-ttu-id="8667d-129">**-p(또는 --subnet-start-ip)**.</span><span class="sxs-lookup"><span data-stu-id="8667d-129">**-p (or --subnet-start-ip)**.</span></span> <span data-ttu-id="8667d-130">서브넷 또는 서브넷 주소 공간의 시작 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="8667d-130">Starting IP address for subnet, or subnet address space.</span></span> <span data-ttu-id="8667d-131">이 시나리오에서는 *192.168.1.0*입니다.</span><span class="sxs-lookup"><span data-stu-id="8667d-131">For our scenario, *192.168.1.0*.</span></span>
   * <span data-ttu-id="8667d-132">**-r(또는 --subnet-cidr)**.</span><span class="sxs-lookup"><span data-stu-id="8667d-132">**-r (or --subnet-cidr)**.</span></span> <span data-ttu-id="8667d-133">서브넷에 대한 CIDR 형식의 네트워크 마스크입니다.</span><span class="sxs-lookup"><span data-stu-id="8667d-133">Network mask in CIDR format for subnet.</span></span> <span data-ttu-id="8667d-134">이 시나리오에서는 *24*입니다.</span><span class="sxs-lookup"><span data-stu-id="8667d-134">For our scenario, *24*.</span></span>
   * <span data-ttu-id="8667d-135">**-l(또는 --location)**.</span><span class="sxs-lookup"><span data-stu-id="8667d-135">**-l (or --location)**.</span></span> <span data-ttu-id="8667d-136">VNet을 만들 Azure 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="8667d-136">Azure region where the VNet is created.</span></span> <span data-ttu-id="8667d-137">이 시나리오에서는 *Central US*입니다.</span><span class="sxs-lookup"><span data-stu-id="8667d-137">For our scenario, *Central US*.</span></span>

3. <span data-ttu-id="8667d-138">서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8667d-138">Create a subnet:</span></span>

    ```azurecli
    azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
    ```
   
    <span data-ttu-id="8667d-139">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="8667d-139">Expected output:</span></span>

            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up the subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK

    <span data-ttu-id="8667d-140">사용된 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="8667d-140">Parameters used:</span></span>

   * <span data-ttu-id="8667d-141">**-t(또는 --vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="8667d-141">**-t (or --vnet-name**.</span></span> <span data-ttu-id="8667d-142">서브넷이 만들어지는 VNet의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="8667d-142">Name of the VNet where the subnet will be created.</span></span> <span data-ttu-id="8667d-143">이 시나리오에서는 *TestVNet*입니다.</span><span class="sxs-lookup"><span data-stu-id="8667d-143">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="8667d-144">**-n(또는 --name)**.</span><span class="sxs-lookup"><span data-stu-id="8667d-144">**-n (or --name)**.</span></span> <span data-ttu-id="8667d-145">새 서브넷의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="8667d-145">Name of the new subnet.</span></span> <span data-ttu-id="8667d-146">이 시나리오에서는 *BackEnd*입니다.</span><span class="sxs-lookup"><span data-stu-id="8667d-146">For our scenario, *BackEnd*.</span></span>
   * <span data-ttu-id="8667d-147">**-a(또는 --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="8667d-147">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="8667d-148">서브넷 CIDR 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="8667d-148">Subnet CIDR block.</span></span> <span data-ttu-id="8667d-149">이 시나리오에서는 *192.168.2.0/24*입니다.</span><span class="sxs-lookup"><span data-stu-id="8667d-149">Four our scenario, *192.168.2.0/24*.</span></span>
   
4. <span data-ttu-id="8667d-150">새 VNet의 속성을 보려면:</span><span class="sxs-lookup"><span data-stu-id="8667d-150">To view the properties of the new VNet:</span></span>

    ```azurecli
    azure network vnet show
    ```
   
    <span data-ttu-id="8667d-151">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="8667d-151">Expected output:</span></span>
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up the virtual network sites
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

## <a name="next-steps"></a><span data-ttu-id="8667d-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8667d-152">Next steps</span></span>

<span data-ttu-id="8667d-153">연결 방법 알아보기:</span><span class="sxs-lookup"><span data-stu-id="8667d-153">Learn how to connect:</span></span>

- <span data-ttu-id="8667d-154">가상 컴퓨터(VM)에서 가상 네트워크 연결은 [Linux VM 만들기](../virtual-machines/linux/quick-create-cli.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8667d-154">A virtual machine (VM) to a virtual network by reading the [Create a Linux VM](../virtual-machines/linux/quick-create-cli.md) article.</span></span> <span data-ttu-id="8667d-155">해당 문서의 단계에서 VNet 및 서브넷을 만드는 대신 기존 VNet 및 서브넷을 VM에 연결하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8667d-155">Instead of creating a VNet and subnet in the steps of the articles, you can select an existing VNet and subnet to connect a VM to.</span></span>
- <span data-ttu-id="8667d-156">가상 네트워크에서 다른 가상 네트워크 연결은 [VNet 연결](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8667d-156">The virtual network to other virtual networks by reading the [Connect VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) article.</span></span>
- <span data-ttu-id="8667d-157">가상 네트워크에서 온-프레미스 네트워크 연결은 사이트 간 VPN(가상 사설망) 또는 ExpressRoute 회로를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8667d-157">The virtual network to an on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="8667d-158">자세한 내용은 [사이트 간 VPN을 사용하여 VNet을 온-프레미스 네트워크에 연결](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) 및 [VNet을 ExpressRoute 회선에 연결](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8667d-158">Learn how by reading the [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>