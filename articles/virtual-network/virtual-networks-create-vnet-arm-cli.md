---
title: "가상 네트워크-Azure CLI 2.0 aaaCreate | Microsoft Docs"
description: "사용 하 여 가상 네트워크 toocreate Azure CLI 2.0 hello 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: e79b7fe780fc81f4866f810d830824e43a5a43b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-hello-azure-cli-20"></a><span data-ttu-id="07e46-103">Hello Azure CLI 2.0을 사용 하 여 가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="07e46-103">Create a virtual network using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="07e46-104">Azure에는 Azure Resource Manager 및 클래식이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07e46-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="07e46-105">Hello 리소스 관리자 배포 모델을 통해 리소스를 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="07e46-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="07e46-106">hello 읽기에 대해 더 알아봅니다 toolearn hello 두 모델 간의 차이 hello [이해 Azure 배포 모델](../azure-resource-manager/resource-manager-deployment-model.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="07e46-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="07e46-107">CLI 버전 toocomplete hello 작업</span><span class="sxs-lookup"><span data-stu-id="07e46-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="07e46-108">Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07e46-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="07e46-109">[Azure CLI 1.0](virtual-networks-create-vnet-cli-nodejs.md) – hello 클래식 및 리소스 관리 배포 모델에 대 한 우리의 CLI</span><span class="sxs-lookup"><span data-stu-id="07e46-109">[Azure CLI 1.0](virtual-networks-create-vnet-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span>
- <span data-ttu-id="07e46-110">[Azure CLI 2.0](#create-a-virtual-network) -우리의 차세대 CLI hello 리소스 관리 배포 모델 (이 문서)에 대 한 '</span><span class="sxs-lookup"><span data-stu-id="07e46-110">[Azure CLI 2.0](#create-a-virtual-network) - our next generation CLI for hello resource management deployment model (this article)\`</span></span>
 
    <span data-ttu-id="07e46-111">리소스 관리자를 통해 다른 도구를 사용 하 여 VNet을 만들 하거나 hello 다음 목록에서에서 다른 옵션을 선택 하 여 hello 클래식 배포 모델을 통해 VNet을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07e46-111">You can also create a VNet through Resource Manager using other tools or create a VNet through hello classic deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="07e46-112">포털</span><span class="sxs-lookup"><span data-stu-id="07e46-112">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
> * [<span data-ttu-id="07e46-113">PowerShell</span><span class="sxs-lookup"><span data-stu-id="07e46-113">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
> * [<span data-ttu-id="07e46-114">CLI</span><span class="sxs-lookup"><span data-stu-id="07e46-114">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
> * [<span data-ttu-id="07e46-115">템플릿</span><span class="sxs-lookup"><span data-stu-id="07e46-115">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
> * [<span data-ttu-id="07e46-116">포털(클래식)</span><span class="sxs-lookup"><span data-stu-id="07e46-116">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
> * [<span data-ttu-id="07e46-117">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="07e46-117">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [<span data-ttu-id="07e46-118">CLI(클래식)</span><span class="sxs-lookup"><span data-stu-id="07e46-118">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]


## <a name="create-a-virtual-network"></a><span data-ttu-id="07e46-119">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="07e46-119">Create a virtual network</span></span>

<span data-ttu-id="07e46-120">사용 하 여 가상 네트워크 toocreate hello Azure CLI 2.0 단계를 수행 하는 전체 hello:</span><span class="sxs-lookup"><span data-stu-id="07e46-120">toocreate a virtual network using hello Azure CLI 2.0, complete hello following steps:</span></span>

1. <span data-ttu-id="07e46-121">설치 하 고 최신 hello 구성 [Azure CLI 2.0](/cli/azure/install-az-cli2) tooan Azure 계정을 사용 하 여 로그인 [az 로그인](/cli/azure/#login)합니다.</span><span class="sxs-lookup"><span data-stu-id="07e46-121">Install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

2. <span data-ttu-id="07e46-122">Hello를 사용 하 여 VNet에 대 한 리소스 그룹 만들기 [az 그룹 만들기](/cli/azure/group#create) hello로 명령을 `--name` 및 `--location` 인수:</span><span class="sxs-lookup"><span data-stu-id="07e46-122">Create a resource group for your VNet using hello [az group create](/cli/azure/group#create) command with hello `--name` and `--location` arguments:</span></span>

    ```azurecli
    az group create --name TestRG --location centralus
    ```

3. <span data-ttu-id="07e46-123">VNet 및 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="07e46-123">Create a VNet and a subnet:</span></span>

    ```azurecli
    az network vnet create \
    --name TestVNet \
    --resource-group TestRG \
    --location centralus \
    --address-prefix 192.168.0.0/16 \
    --subnet-name FrontEnd \
    --subnet-prefix 192.168.1.0/24
    ```

    <span data-ttu-id="07e46-124">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="07e46-124">Expected output:</span></span>
    
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

    <span data-ttu-id="07e46-125">사용된 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="07e46-125">Parameters used:</span></span>

    - <span data-ttu-id="07e46-126">`--name TestVNet`: Hello VNet toobe 생성의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="07e46-126">`--name TestVNet`: Name of hello VNet toobe created.</span></span>
    - <span data-ttu-id="07e46-127">`--resource-group TestRG`: hello 리소스를 제어 하는 # hello 리소스 그룹 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="07e46-127">`--resource-group TestRG`: # hello resource group name that controls hello resource.</span></span> 
    - <span data-ttu-id="07e46-128">`--location centralus`: hello 어떤 toodeploy에 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e46-128">`--location centralus`: hello location into which toodeploy.</span></span>
    - <span data-ttu-id="07e46-129">`--address-prefix 192.168.0.0/16`: hello 주소 접두사와 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="07e46-129">`--address-prefix 192.168.0.0/16`: hello address prefix and block.</span></span>  
    - <span data-ttu-id="07e46-130">`--subnet-name FrontEnd`: hello 서브넷의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="07e46-130">`--subnet-name FrontEnd`: hello name of hello subnet.</span></span>
    - <span data-ttu-id="07e46-131">`--subnet-prefix 192.168.1.0/24`: hello 주소 접두사와 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="07e46-131">`--subnet-prefix 192.168.1.0/24`: hello address prefix and block.</span></span>

    <span data-ttu-id="07e46-132">toolist hello 기본 정보 toouse hello에서 다음 명령을 사용 하 여 hello VNet을 쿼리할 수 있습니다는 [쿼리 필터](/cli/azure/query-az-cli2):</span><span class="sxs-lookup"><span data-stu-id="07e46-132">toolist hello basic information toouse in hello next command, you can query hello VNet using a [query filter](/cli/azure/query-az-cli2):</span></span>

    ```azurecli
    az network vnet list --query '[?name==`TestVNet`].{Where:location,Name:name,Group:resourceGroup}' -o table
    ```

    <span data-ttu-id="07e46-133">hello 다음 출력을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e46-133">Which produces hello following output:</span></span>

        Where      Name      Group

        centralus  TestVNet  TestRG

4. <span data-ttu-id="07e46-134">서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="07e46-134">Create a subnet:</span></span>

    ```azurecli
    az network vnet subnet create \
    --address-prefix 192.168.2.0/24 \
    --name BackEnd \
    --resource-group TestRG \
    --vnet-name TestVNet
    ```

    <span data-ttu-id="07e46-135">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="07e46-135">Expected output:</span></span>

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

    <span data-ttu-id="07e46-136">사용된 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="07e46-136">Parameters used:</span></span>

    - <span data-ttu-id="07e46-137">`--address-prefix 192.168.2.0/24`: 서브넷 CIDR 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="07e46-137">`--address-prefix 192.168.2.0/24`: Subnet CIDR block.</span></span>
    - <span data-ttu-id="07e46-138">`--name BackEnd`: Hello 새 서브넷의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="07e46-138">`--name BackEnd`: Name of hello new subnet.</span></span>
    - <span data-ttu-id="07e46-139">`--resource-group TestRG`: hello 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="07e46-139">`--resource-group TestRG`: hello resource group.</span></span>
    - <span data-ttu-id="07e46-140">`--vnet-name TestVNet`: hello 이름 VNet을 소유 하는 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="07e46-140">`--vnet-name TestVNet`: hello name of hello owning VNet.</span></span>

5. <span data-ttu-id="07e46-141">쿼리 hello 속성을 새 VNet을 hello:</span><span class="sxs-lookup"><span data-stu-id="07e46-141">Query hello properties of hello new VNet:</span></span>

    ```azurecli
    az network vnet show \
    -g TestRG \
    -n TestVNet \
    --query '{Name:name,Where:location,Group:resourceGroup,Status:provisioningState,SubnetCount:subnets | length(@)}' \
    -o table
    ```

    <span data-ttu-id="07e46-142">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="07e46-142">Expected output:</span></span>

        Name      Where      Group    Status       SubnetCount

        TestVNet  centralus  TestRG   Succeeded              2

6. <span data-ttu-id="07e46-143">Hello 서브넷의 쿼리 hello 속성:</span><span class="sxs-lookup"><span data-stu-id="07e46-143">Query hello properties of hello subnets:</span></span>

    ```azurecli
    az network vnet subnet list \
    -g TestRG \
    --vnet-name testvnet \
    --query '[].{Name:name,CIDR:addressPrefix,Status:provisioningState}' \
    -o table
    ```

    <span data-ttu-id="07e46-144">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="07e46-144">Expected output:</span></span>

        Name      CIDR            Status

        FrontEnd  192.168.1.0/24  Succeeded
        BackEnd   192.168.2.0/24  Succeeded

## <a name="next-steps"></a><span data-ttu-id="07e46-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="07e46-145">Next steps</span></span>

<span data-ttu-id="07e46-146">자세한 내용은 방법 tooconnect:</span><span class="sxs-lookup"><span data-stu-id="07e46-146">Learn how tooconnect:</span></span>

- <span data-ttu-id="07e46-147">Hello를 참조 하 여 가상 컴퓨터 (VM) tooa 가상 네트워크 [Linux VM을 만들](../virtual-machines/linux/quick-create-cli.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="07e46-147">A virtual machine (VM) tooa virtual network by reading hello [Create a Linux VM](../virtual-machines/linux/quick-create-cli.md) article.</span></span> <span data-ttu-id="07e46-148">Hello 아티클의 hello 단계에서 VNet 및 서브넷을 만드는 대신 및 선택할 수 있습니다는 기존 VNet 서브넷 tooconnect VM을 합니다.</span><span class="sxs-lookup"><span data-stu-id="07e46-148">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="07e46-149">hello를 참조 하 여 가상 네트워크 tooother 가상 네트워크를 hello [Vnet 연결](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="07e46-149">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) article.</span></span>
- <span data-ttu-id="07e46-150">가상 네트워크 tooan hello 온-프레미스 사이트 간 가상 사설망 (VPN) 또는 express 경로 회로 사용 하 여 네트워크.</span><span class="sxs-lookup"><span data-stu-id="07e46-150">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="07e46-151">자세한 방법은 hello [사이트 간 VPN을 사용 하 여 VNet tooan 온-프레미스 네트워크 연결](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) 및 [VNet tooan ExpressRoute 회로 연결](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="07e46-151">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>
