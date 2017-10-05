---
title: "네트워크 보안 그룹 만들기 - Azure CLI 2.0 | Microsoft Docs"
description: "Azure CLI 2.0을 사용하여 네트워크 보안 그룹을 만들고 배포하는 방법을 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9ea82c09-f4a6-4268-88bc-fc439db40c48
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/17/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8efb3ab66d07875b51f723fed5594bcb477ed025
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-network-security-groups-using-the-azure-cli-20"></a><span data-ttu-id="3b48e-103">Azure CLI 2.0을 사용하여 네트워크 보안 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="3b48e-103">Create network security groups using the Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="3b48e-104">태스크를 완료하기 위한 CLI 버전</span><span class="sxs-lookup"><span data-stu-id="3b48e-104">CLI versions to complete the task</span></span> 

<span data-ttu-id="3b48e-105">다음 CLI 버전 중 하나를 사용하여 태스크를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b48e-105">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="3b48e-106">[Azure CLI 1.0](virtual-networks-create-nsg-cli-nodejs.md) - 클래식 및 리소스 관리 배포 모델용 CLI</span><span class="sxs-lookup"><span data-stu-id="3b48e-106">[Azure CLI 1.0](virtual-networks-create-nsg-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span> 
- <span data-ttu-id="3b48e-107">[Azure CLI 2.0](#Create-the-nsg-for-the-front-end-subnet) - 리소스 관리 배포 모델용 차세대 CLI(이 문서)</span><span class="sxs-lookup"><span data-stu-id="3b48e-107">[Azure CLI 2.0](#Create-the-nsg-for-the-front-end-subnet) - our next generation CLI for the resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="3b48e-108">다음 샘플 Azure CLI 2.0 명령에는 앞의 시나리오를 기반으로 이미 만들어져 있는 단순한 환경이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3b48e-108">The sample Azure CLI 2.0 commands following expect a simple environment already created based on the scenario preceding.</span></span> 

## <a name="create-the-nsg-for-the-frontend-subnet"></a><span data-ttu-id="3b48e-109">`FrontEnd` 서브넷에 대한 NSG 만들기</span><span class="sxs-lookup"><span data-stu-id="3b48e-109">Create the NSG for the `FrontEnd` subnet</span></span>

<span data-ttu-id="3b48e-110">앞의 시나리오에 따라 *NSG-FrontEnd*라는 NSG를 만들려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="3b48e-110">To create an NSG named *NSG-FrontEnd* based on the scenario preceding, follow the steps following.</span></span>

1. <span data-ttu-id="3b48e-111">아직 설치하지 않은 경우 최신 [Azure CLI 2.0](/cli/azure/install-az-cli2)을 설치 및 구성하고 [az login](/cli/azure/#login)을 사용하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="3b48e-111">If you haven't yet, install and configure the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span> 

2. <span data-ttu-id="3b48e-112">[az network nsg create](/cli/azure/network/nsg#create) 명령을 실행하여 NSG를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3b48e-112">Create an NSG using the [az network nsg create](/cli/azure/network/nsg#create) command.</span></span> 

    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-FrontEnd \
    --location centralus 
    ```

    <span data-ttu-id="3b48e-113">매개 변수:</span><span class="sxs-lookup"><span data-stu-id="3b48e-113">Parameters:</span></span>
   
   * <span data-ttu-id="3b48e-114">`--resource-group`: NSG가 만들어지는 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b48e-114">`--resource-group`: Name of the resource group where the NSG is created.</span></span> <span data-ttu-id="3b48e-115">이 시나리오에서는 *TestRG*입니다.</span><span class="sxs-lookup"><span data-stu-id="3b48e-115">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="3b48e-116">`--location`: 새 NSG를 만들 Azure 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="3b48e-116">`--location`: Azure region where the new NSG is created.</span></span> <span data-ttu-id="3b48e-117">이 시나리오에서는 *westus*입니다.</span><span class="sxs-lookup"><span data-stu-id="3b48e-117">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="3b48e-118">`--name`: 새 NSG의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b48e-118">`--name`: Name for the new NSG.</span></span> <span data-ttu-id="3b48e-119">이 시나리오에서는 *NSG-FrontEnd*입니다.</span><span class="sxs-lookup"><span data-stu-id="3b48e-119">For our scenario, *NSG-FrontEnd*.</span></span>

    <span data-ttu-id="3b48e-120">예상된 출력에는 모든 기본 규칙 목록을 포함하여 매우 많은 정보가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b48e-120">The expected output is quite a bit of information including a list of all the default rules.</span></span> <span data-ttu-id="3b48e-121">다음 예제에서는 JMESPATH 쿼리 필터를 사용하여 `table` 출력 형식으로 기본 규칙을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3b48e-121">The following example shows the default rules using a JMESPATH query filter with the `table` output format:</span></span>

    ```azurecli
    az network nsg show \
    -g testrg \
    -n nsg-frontend \
    --query 'defaultSecurityRules[].{Access:access,Desc:description,DestPortRange:destinationPortRange,Direction:direction,Priority:priority}' \
    -o table
    ```
   
   <span data-ttu-id="3b48e-122">출력</span><span class="sxs-lookup"><span data-stu-id="3b48e-122">Output:</span></span>

        Access    Desc                                                    DestPortRange    Direction      Priority
        
        Allow     Allow inbound traffic from all VMs in VNET              *                Inbound           65000
        Allow     Allow inbound traffic from azure load balancer          *                Inbound           65001
        Deny      Deny all inbound traffic                                *                Inbound           65500
        Allow     Allow outbound traffic from all VMs to all VMs in VNET  *                Outbound          65000
        Allow     Allow outbound traffic from all VMs to Internet         *                Outbound          65001
        Deny      Deny all outbound traffic                               *                Outbound          65500



3. <span data-ttu-id="3b48e-123">[az network nsg rule create](/cli/azure/network/nsg/rule#create) 명령을 실행하여 인터넷에서 포트 3389(RDP)에 대한 액세스를 허용하는 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3b48e-123">Create a rule that allows access to port 3389 (RDP) from the Internet with the [az network nsg rule create](/cli/azure/network/nsg/rule#create) command.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3b48e-124">사용하는 셸에 따라 인수를 실행하기 전에 확장하지 못하도록 다음 인수에서 `*` 문자를 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b48e-124">Depending on the shell you are using, you might need to modify the `*` character in the arguments following so as not to expand the argument before execution.</span></span>
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-FrontEnd \
    --name rdp-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix Internet \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 3389
    ```
   
    <span data-ttu-id="3b48e-125">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="3b48e-125">Expected output:</span></span>
   
    ```json
    {
        "access": "Allow",
        "description": null,
        "destinationAddressPrefix": "*",
        "destinationPortRange": "3389",
        "direction": "Inbound",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule",
        "name": "rdp-rule",
        "priority": 100,
        "protocol": "Tcp",
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "sourceAddressPrefix": "Internet",
        "sourcePortRange": "*"
    }
    ```

    <span data-ttu-id="3b48e-126">매개 변수:</span><span class="sxs-lookup"><span data-stu-id="3b48e-126">Parameters:</span></span>

    * <span data-ttu-id="3b48e-127">`--resource-group testrg`: 사용할 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="3b48e-127">`--resource-group testrg`: The resource group to use.</span></span> <span data-ttu-id="3b48e-128">대/소문자를 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3b48e-128">Note that it is case-insensitive.</span></span>
    * <span data-ttu-id="3b48e-129">`--nsg-name NSG-FrontEnd`: 규칙이 만들어질 NSG의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b48e-129">`--nsg-name NSG-FrontEnd`: Name of the NSG in which the rule is created.</span></span>
    * <span data-ttu-id="3b48e-130">`--name rdp-rule`: 새 규칙의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b48e-130">`--name rdp-rule`: Name for the new rule.</span></span>
    * <span data-ttu-id="3b48e-131">`--access Allow`: 규칙(허용 또는 거부)에 대한 액세스 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="3b48e-131">`--access Allow`: Access level for the rule (Deny or Allow).</span></span>
    * <span data-ttu-id="3b48e-132">`--protocol Tcp`: 프로토콜(Tcp, Udp 또는 *)입니다.</span><span class="sxs-lookup"><span data-stu-id="3b48e-132">`--protocol Tcp`: Protocol (Tcp, Udp, or *).</span></span>
    * <span data-ttu-id="3b48e-133">`--direction Inbound`: 연결 방향(인바운드 또는 아웃바운드)입니다.</span><span class="sxs-lookup"><span data-stu-id="3b48e-133">`--direction Inbound`: Direction of the connection (Inbound or Outbound).</span></span>
    * <span data-ttu-id="3b48e-134">`--priority 100`: 규칙에 대한 우선순위입니다.</span><span class="sxs-lookup"><span data-stu-id="3b48e-134">`--priority 100`: Priority for the rule.</span></span>
    * <span data-ttu-id="3b48e-135">`--source-address-prefix Internet`: CIDR 또는 기본 태그를 사용하는 원본 주소 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="3b48e-135">`--source-address-prefix Internet`: Source address prefix in CIDR or using default tags.</span></span>
    * <span data-ttu-id="3b48e-136">`--source-port-range "*"`: 원본 포트 또는 포트 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="3b48e-136">`--source-port-range "*"`: Source port or port range.</span></span> <span data-ttu-id="3b48e-137">연결을 여는 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="3b48e-137">Port that opened the connection.</span></span>
    * <span data-ttu-id="3b48e-138">`--destination-address-prefix "*"`: CIDR 또는 기본 태그를 사용하는 대상 주소 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="3b48e-138">`--destination-address-prefix "*"`: Destination address prefix in CIDR or using default tags.</span></span>
    * <span data-ttu-id="3b48e-139">`--destination-port-range 3389`: 대상 포트 또는 포트 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="3b48e-139">`--destination-port-range 3389`: Destination port or port range.</span></span> <span data-ttu-id="3b48e-140">연결 요쳥을 수신하는 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="3b48e-140">Port that receives the connection request.</span></span>



4. <span data-ttu-id="3b48e-141">**az network nsg rule create** 명령을 실행하여 인터넷에서 포트 80(HTTP)에 대한 액세스를 허용하는 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3b48e-141">Create a rule that allows access to port 80 (HTTP) from the Internet **az network nsg rule create** command.</span></span>
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-FrontEnd \
    --name web-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 200 \
    --source-address-prefix Internet \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 80
    ```
   
    <span data-ttu-id="3b48e-142">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="3b48e-142">Expected putput:</span></span>
   
    ```json
    {
        "access": "Allow",
        "description": null,
        "destinationAddressPrefix": "*",
        "destinationPortRange": "80",
        "direction": "Inbound",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule",
        "name": "web-rule",
        "priority": 200,
        "protocol": "Tcp",
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "sourceAddressPrefix": "Internet",
        "sourcePortRange": "*"
    }
    ```

5. <span data-ttu-id="3b48e-143">[az network vnet subnet update](/cli/azure/network/vnet/subnet#update) 명령을 사용하여 NSG를 **FrontEnd** 서브넷에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="3b48e-143">Bind the NSG to the **FrontEnd** subnet with the [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) command.</span></span>
        
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name FrontEnd \
    --resource-group testrg \
    --network-security-group NSG-FrontEnd
    ```
   
    <span data-ttu-id="3b48e-144">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="3b48e-144">Expected output:</span></span>
   
    ```json
    {
        "addressPrefix": "192.168.1.0/24",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/TestVNET/subnets/FrontEnd",
        "ipConfigurations": [
            {
            "etag": null,
            "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
            "name": null,
            "privateIpAddress": null,
            "privateIpAllocationMethod": null,
            "provisioningState": null,
            "publicIpAddress": null,
            "resourceGroup": "TestRG",
            "subnet": null
            }
        ],
        "name": "FrontEnd",
        "networkSecurityGroup": {
            "defaultSecurityRules": null,
            "etag": null,
            "id": "/subscriptions/<guid>f/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd",
            "location": null,
            "name": null,
            "networkInterfaces": null,
            "provisioningState": null,
            "resourceGroup": "testrg",
            "resourceGuid": null,
            "securityRules": null,
            "subnets": null,
            "tags": null,
            "type": null
        },
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "resourceNavigationLinks": null,
        "routeTable": null
    }
    ```

## <a name="create-the-nsg-for-the-backend-subnet"></a><span data-ttu-id="3b48e-145">`BackEnd` 서브넷에 대한 NSG 만들기</span><span class="sxs-lookup"><span data-stu-id="3b48e-145">Create the NSG for the `BackEnd` subnet</span></span>
<span data-ttu-id="3b48e-146">앞의 시나리오에 따라 *NSG-BackEnd*라는 NSG를 만들려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="3b48e-146">To create an NSG named *NSG-BackEnd* based on the scenario preceding, follow the steps following.</span></span>

1. <span data-ttu-id="3b48e-147">**az network nsg create**를 사용하여 `NSG-BackEnd` NSG를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3b48e-147">Create the `NSG-BackEnd` NSG with **az network nsg create**.</span></span>
   
    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-BackEnd \
    --location centralus
    ```
   
    <span data-ttu-id="3b48e-148">앞서 2단계와 마찬가지로 예상된 출력은 기본 규칙을 포함하여 매우 큽니다.</span><span class="sxs-lookup"><span data-stu-id="3b48e-148">As in step 2, preceding, the expected output is quite large, including default rules.</span></span>
   
2. <span data-ttu-id="3b48e-149">**az network nsg rule create** 명령을 실행하여 `FrontEnd` 서브넷에서 포트 1433(SQL)에 대한 액세스를 허용하는 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3b48e-149">Create a rule that allows access to port 1433 (SQL) from the `FrontEnd` subnet with the **az network nsg rule create** command.</span></span>
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-BackEnd \
    --name sql-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix 192.168.1.0/24 \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 1433
    ```
   
    <span data-ttu-id="3b48e-150">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="3b48e-150">Expected output:</span></span>

    ```json  
    {
    "access": "Allow",
    "description": null,
    "destinationAddressPrefix": "*",
    "destinationPortRange": "1433",
    "direction": "Inbound",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/sql-rule",
    "name": "sql-rule",
    "priority": 100,
    "protocol": "Tcp",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "sourceAddressPrefix": "192.168.1.0/24",
    "sourcePortRange": "*"
    }
    ```

3. <span data-ttu-id="3b48e-151">**az network nsg rule create** 명령을 사용하여 인터넷에 대한 액세스를 거부하는 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3b48e-151">Create a rule that denies access to the Internet using the **az network nsg rule create** command.</span></span>
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-BackEnd \
    --name web-rule \
    --access Deny \
    --protocol Tcp  \
    --direction Outbound  \
    --priority 200 \
    --source-address-prefix "*" \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range "*"
    ```
   
    <span data-ttu-id="3b48e-152">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="3b48e-152">Expected putput:</span></span>
   
    ```json
    {
    "access": "Deny",
    "description": null,
    "destinationAddressPrefix": "*",
    "destinationPortRange": "*",
    "direction": "Outbound",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/web-rule",
    "name": "web-rule",
    "priority": 200,
    "protocol": "Tcp",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "sourceAddressPrefix": "*",
    "sourcePortRange": "*"
    }
    ```

4. <span data-ttu-id="3b48e-153">**az network vnet subnet set** 명령을 사용하여 NSG를 `BackEnd` 서브넷에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="3b48e-153">Bind the NSG to the `BackEnd` subnet using the **az network vnet subnet set** command.</span></span>
   
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name BackEnd \
    --resource-group testrg \
    --network-security-group NSG-BackEnd
    ```
   
    <span data-ttu-id="3b48e-154">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="3b48e-154">Expected output:</span></span>
   
    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/TestVNET/subnets/BackEnd",
    "ipConfigurations": null,
    "name": "BackEnd",
    "networkSecurityGroup": {
        "defaultSecurityRules": null,
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd",
        "location": null,
        "name": null,
        "networkInterfaces": null,
        "provisioningState": null,
        "resourceGroup": "testrg",
        "resourceGuid": null,
        "securityRules": null,
        "subnets": null,
        "tags": null,
        "type": null
    },
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "resourceNavigationLinks": null,
    "routeTable": null
    }
    ```
