---
title: "가상 네트워크 만들기 - Azure CLI 2.0 | Microsoft Docs"
description: "Azure CLI 2.0을 사용하여 가상 네트워크를 만드는 방법을 알아봅니다."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 75966bcc-0056-4667-8482-6f08ca38e77a
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c7d7b3543f488aedff1ea2c68a2b497e0ca744af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-network-using-the-azure-cli-20"></a><span data-ttu-id="9ab70-103">Azure CLI 2.0을 사용하여 가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="9ab70-103">Create a virtual network using the Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="9ab70-104">Azure에는 Azure Resource Manager 및 클래식이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ab70-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="9ab70-105">Resource Manager 배포 모델을 통해 리소스를 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9ab70-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="9ab70-106">두 가지 모델의 차이점에 대해 자세히 알아보려면 [Azure 배포 모델 이해](../azure-resource-manager/resource-manager-deployment-model.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9ab70-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="9ab70-107">태스크를 완료하기 위한 CLI 버전</span><span class="sxs-lookup"><span data-stu-id="9ab70-107">CLI versions to complete the task</span></span>
<span data-ttu-id="9ab70-108">다음 CLI 버전 중 하나를 사용하여 태스크를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ab70-108">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="9ab70-109">[Azure CLI 1.0](virtual-networks-create-vnet-cli-nodejs.md) - 클래식 및 리소스 관리 배포 모델용 CLI</span><span class="sxs-lookup"><span data-stu-id="9ab70-109">[Azure CLI 1.0](virtual-networks-create-vnet-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span>
- <span data-ttu-id="9ab70-110">[Azure CLI 2.0](#create-a-virtual-network) - 리소스 관리 배포 모델용 차세대 CLI(이 문서)</span><span class="sxs-lookup"><span data-stu-id="9ab70-110">[Azure CLI 2.0](#create-a-virtual-network) - our next generation CLI for the resource management deployment model (this article)\`</span></span>
 
    <span data-ttu-id="9ab70-111">다른 도구를 사용하여 Resource Manager를 통해 VNet을 만들거나 다음 목록에서 다른 옵션을 선택하여 클래식 배포 모델을 통해 VNet을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ab70-111">You can also create a VNet through Resource Manager using other tools or create a VNet through the classic deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9ab70-112">포털</span><span class="sxs-lookup"><span data-stu-id="9ab70-112">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
> * [<span data-ttu-id="9ab70-113">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9ab70-113">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
> * [<span data-ttu-id="9ab70-114">CLI</span><span class="sxs-lookup"><span data-stu-id="9ab70-114">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
> * [<span data-ttu-id="9ab70-115">템플릿</span><span class="sxs-lookup"><span data-stu-id="9ab70-115">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
> * [<span data-ttu-id="9ab70-116">포털(클래식)</span><span class="sxs-lookup"><span data-stu-id="9ab70-116">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
> * [<span data-ttu-id="9ab70-117">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="9ab70-117">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [<span data-ttu-id="9ab70-118">CLI(클래식)</span><span class="sxs-lookup"><span data-stu-id="9ab70-118">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]


## <a name="create-a-virtual-network"></a><span data-ttu-id="9ab70-119">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="9ab70-119">Create a virtual network</span></span>

<span data-ttu-id="9ab70-120">Azure CLI 2.0을 사용하여 가상 네트워크를 만들려면 다음 단계를 완료하세요.</span><span class="sxs-lookup"><span data-stu-id="9ab70-120">To create a virtual network using the Azure CLI 2.0, complete the following steps:</span></span>

1. <span data-ttu-id="9ab70-121">최신 [Azure CLI 2.0](/cli/azure/install-az-cli2)을 설치 및 구성하고 [az login](/cli/azure/#login)을 사용하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9ab70-121">Install and configure the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span>

2. <span data-ttu-id="9ab70-122">`--name` 및 `--location` 인수를 포함한 [az group create](/cli/azure/group#create) 명령을 사용하여 VNet에 대한 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9ab70-122">Create a resource group for your VNet using the [az group create](/cli/azure/group#create) command with the `--name` and `--location` arguments:</span></span>

    ```azurecli
    az group create --name TestRG --location centralus
    ```

3. <span data-ttu-id="9ab70-123">VNet 및 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9ab70-123">Create a VNet and a subnet:</span></span>

    ```azurecli
    az network vnet create \
    --name TestVNet \
    --resource-group TestRG \
    --location centralus \
    --address-prefix 192.168.0.0/16 \
    --subnet-name FrontEnd \
    --subnet-prefix 192.168.1.0/24
    ```

    <span data-ttu-id="9ab70-124">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="9ab70-124">Expected output:</span></span>
    
    ```json
    {
        "newVNet": {
            "addressSpace": {
            "addressPrefixes": [
            "192.168.0.0/16"
            ]
            },
            "dhcpOptions": {
            "dnsServers": []
            },
            "provisioningState": "Succeeded",
            "resourceGuid": "<guid>",
            "subnets": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                "name": "FrontEnd",
                "properties": {
                "addressPrefix": "192.168.1.0/24",
                "provisioningState": "Succeeded"
                },
                "resourceGroup": "TestRG"
            }
            ]
            }
    }
    ```

    <span data-ttu-id="9ab70-125">사용된 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="9ab70-125">Parameters used:</span></span>

    - <span data-ttu-id="9ab70-126">`--name TestVNet`: 만들 VNet의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9ab70-126">`--name TestVNet`: Name of the VNet to be created.</span></span>
    - <span data-ttu-id="9ab70-127">`--resource-group TestRG`: # 리소스를 제어하는 리소스 그룹 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9ab70-127">`--resource-group TestRG`: # The resource group name that controls the resource.</span></span> 
    - <span data-ttu-id="9ab70-128">`--location centralus`: 배포할 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="9ab70-128">`--location centralus`: The location into which to deploy.</span></span>
    - <span data-ttu-id="9ab70-129">`--address-prefix 192.168.0.0/16`: 주소 접두사와 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="9ab70-129">`--address-prefix 192.168.0.0/16`: The address prefix and block.</span></span>  
    - <span data-ttu-id="9ab70-130">`--subnet-name FrontEnd`: 서브넷의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9ab70-130">`--subnet-name FrontEnd`: The name of the subnet.</span></span>
    - <span data-ttu-id="9ab70-131">`--subnet-prefix 192.168.1.0/24`: 주소 접두사와 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="9ab70-131">`--subnet-prefix 192.168.1.0/24`: The address prefix and block.</span></span>

    <span data-ttu-id="9ab70-132">다음 명령에서 사용할 기본 정보를 나열하려면 [쿼리 필터](/cli/azure/query-az-cli2)를 사용하여 VNet을 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ab70-132">To list the basic information to use in the next command, you can query the VNet using a [query filter](/cli/azure/query-az-cli2):</span></span>

    ```azurecli
    az network vnet list --query '[?name==`TestVNet`].{Where:location,Name:name,Group:resourceGroup}' -o table
    ```

    <span data-ttu-id="9ab70-133">다음과 같은 출력을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="9ab70-133">Which produces the following output:</span></span>

        Where      Name      Group

        centralus  TestVNet  TestRG

4. <span data-ttu-id="9ab70-134">서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9ab70-134">Create a subnet:</span></span>

    ```azurecli
    az network vnet subnet create \
    --address-prefix 192.168.2.0/24 \
    --name BackEnd \
    --resource-group TestRG \
    --vnet-name TestVNet
    ```

    <span data-ttu-id="9ab70-135">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="9ab70-135">Expected output:</span></span>

    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid> \"",
    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
    "ipConfigurations": null,
    "name": "BackEnd",
    "networkSecurityGroup": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "TestRG",
    "resourceNavigationLinks": null,
    "routeTable": null
    }
    ```

    <span data-ttu-id="9ab70-136">사용된 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="9ab70-136">Parameters used:</span></span>

    - <span data-ttu-id="9ab70-137">`--address-prefix 192.168.2.0/24`: 서브넷 CIDR 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="9ab70-137">`--address-prefix 192.168.2.0/24`: Subnet CIDR block.</span></span>
    - <span data-ttu-id="9ab70-138">`--name BackEnd`: 새 서브넷의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9ab70-138">`--name BackEnd`: Name of the new subnet.</span></span>
    - <span data-ttu-id="9ab70-139">`--resource-group TestRG`: 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="9ab70-139">`--resource-group TestRG`: The resource group.</span></span>
    - <span data-ttu-id="9ab70-140">`--vnet-name TestVNet`: 소유한 VNet의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9ab70-140">`--vnet-name TestVNet`: The name of the owning VNet.</span></span>

5. <span data-ttu-id="9ab70-141">새 VNet의 속성을 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="9ab70-141">Query the properties of the new VNet:</span></span>

    ```azurecli
    az network vnet show \
    -g TestRG \
    -n TestVNet \
    --query '{Name:name,Where:location,Group:resourceGroup,Status:provisioningState,SubnetCount:subnets | length(@)}' \
    -o table
    ```

    <span data-ttu-id="9ab70-142">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="9ab70-142">Expected output:</span></span>

        Name      Where      Group    Status       SubnetCount

        TestVNet  centralus  TestRG   Succeeded              2

6. <span data-ttu-id="9ab70-143">서브넷의 속성을 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="9ab70-143">Query the properties of the subnets:</span></span>

    ```azurecli
    az network vnet subnet list \
    -g TestRG \
    --vnet-name testvnet \
    --query '[].{Name:name,CIDR:addressPrefix,Status:provisioningState}' \
    -o table
    ```

    <span data-ttu-id="9ab70-144">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="9ab70-144">Expected output:</span></span>

        Name      CIDR            Status

        FrontEnd  192.168.1.0/24  Succeeded
        BackEnd   192.168.2.0/24  Succeeded

## <a name="next-steps"></a><span data-ttu-id="9ab70-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9ab70-145">Next steps</span></span>

<span data-ttu-id="9ab70-146">연결 방법 알아보기:</span><span class="sxs-lookup"><span data-stu-id="9ab70-146">Learn how to connect:</span></span>

- <span data-ttu-id="9ab70-147">가상 컴퓨터(VM)에서 가상 네트워크 연결은 [Linux VM 만들기](../virtual-machines/linux/quick-create-cli.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9ab70-147">A virtual machine (VM) to a virtual network by reading the [Create a Linux VM](../virtual-machines/linux/quick-create-cli.md) article.</span></span> <span data-ttu-id="9ab70-148">해당 문서의 단계에서 VNet 및 서브넷을 만드는 대신 기존 VNet 및 서브넷을 VM에 연결하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ab70-148">Instead of creating a VNet and subnet in the steps of the articles, you can select an existing VNet and subnet to connect a VM to.</span></span>
- <span data-ttu-id="9ab70-149">가상 네트워크에서 다른 가상 네트워크 연결은 [VNet 연결](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9ab70-149">The virtual network to other virtual networks by reading the [Connect VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) article.</span></span>
- <span data-ttu-id="9ab70-150">가상 네트워크에서 온-프레미스 네트워크 연결은 사이트 간 VPN(가상 사설망) 또는 ExpressRoute 회로를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9ab70-150">The virtual network to an on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="9ab70-151">자세한 내용은 [사이트 간 VPN을 사용하여 VNet을 온-프레미스 네트워크에 연결](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) 및 [VNet을 ExpressRoute 회선에 연결](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9ab70-151">Learn how by reading the [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>