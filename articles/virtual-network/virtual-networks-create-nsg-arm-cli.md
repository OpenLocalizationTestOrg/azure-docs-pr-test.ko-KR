---
title: "aaaCreate 네트워크 보안 그룹-Azure CLI 2.0 | Microsoft Docs"
description: "자세한 방법을 toocreate hello Azure CLI 2.0을 사용 하 여 네트워크 보안 그룹을 배포 합니다."
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
ms.openlocfilehash: 30b1d60676331bf5e2bbbb046c747477be9d3338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-hello-azure-cli-20"></a><span data-ttu-id="4f537-103">네트워크를 Azure CLI 2.0 hello를 사용 하 여 보안 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="4f537-103">Create network security groups using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="4f537-104">CLI 버전 toocomplete hello 작업</span><span class="sxs-lookup"><span data-stu-id="4f537-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="4f537-105">Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f537-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="4f537-106">[Azure CLI 1.0](virtual-networks-create-nsg-cli-nodejs.md) – hello 클래식 및 리소스 관리 배포 모델에 대 한 우리의 CLI</span><span class="sxs-lookup"><span data-stu-id="4f537-106">[Azure CLI 1.0](virtual-networks-create-nsg-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="4f537-107">[Azure CLI 2.0](#Create-the-nsg-for-the-front-end-subnet) -우리의 차세대 CLI hello 리소스 관리 배포 모델 (이 문서)</span><span class="sxs-lookup"><span data-stu-id="4f537-107">[Azure CLI 2.0](#Create-the-nsg-for-the-front-end-subnet) - our next generation CLI for hello resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="4f537-108">hello 샘플 Azure CLI 2.0 다음 이미 이전 hello 시나리오를 기반으로 만들어진 단순 환경 예상 되는 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="4f537-108">hello sample Azure CLI 2.0 commands following expect a simple environment already created based on hello scenario preceding.</span></span> 

## <a name="create-hello-nsg-for-hello-frontend-subnet"></a><span data-ttu-id="4f537-109">Hello에 대 한 hello NSG 만들기 `FrontEnd` 서브넷</span><span class="sxs-lookup"><span data-stu-id="4f537-109">Create hello NSG for hello `FrontEnd` subnet</span></span>

<span data-ttu-id="4f537-110">명명 된 NSG toocreate *NSG 프런트 엔드* hello 단계 다음에 따라 이전 hello 시나리오에 따라, 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f537-110">toocreate an NSG named *NSG-FrontEnd* based on hello scenario preceding, follow hello steps following.</span></span>

1. <span data-ttu-id="4f537-111">하지 않은 아직 설치 하 고 최신 hello 구성 [Azure CLI 2.0](/cli/azure/install-az-cli2) tooan Azure 계정을 사용 하 여 로그인 [az 로그인](/cli/azure/#login)합니다.</span><span class="sxs-lookup"><span data-stu-id="4f537-111">If you haven't yet, install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span> 

2. <span data-ttu-id="4f537-112">Hello를 사용 하 여 NSG 만들기 [az 네트워크 nsg 만들기](/cli/azure/network/nsg#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="4f537-112">Create an NSG using hello [az network nsg create](/cli/azure/network/nsg#create) command.</span></span> 

    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-FrontEnd \
    --location centralus 
    ```

    <span data-ttu-id="4f537-113">매개 변수</span><span class="sxs-lookup"><span data-stu-id="4f537-113">Parameters:</span></span>
   
   * <span data-ttu-id="4f537-114">`--resource-group`: Hello NSG를 만들 위치 hello 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4f537-114">`--resource-group`: Name of hello resource group where hello NSG is created.</span></span> <span data-ttu-id="4f537-115">이 시나리오에서는 *TestRG*입니다.</span><span class="sxs-lookup"><span data-stu-id="4f537-115">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="4f537-116">`--location`: Azure 영역 hello 새 NSG를 만들 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="4f537-116">`--location`: Azure region where hello new NSG is created.</span></span> <span data-ttu-id="4f537-117">이 시나리오에서는 *westus*입니다.</span><span class="sxs-lookup"><span data-stu-id="4f537-117">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="4f537-118">`--name`: 이름 hello에 대 한 새 NSG 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f537-118">`--name`: Name for hello new NSG.</span></span> <span data-ttu-id="4f537-119">이 시나리오에서는 *NSG-FrontEnd*입니다.</span><span class="sxs-lookup"><span data-stu-id="4f537-119">For our scenario, *NSG-FrontEnd*.</span></span>

    <span data-ttu-id="4f537-120">hello 출력은 모든 hello 기본 규칙의 목록을 포함 하 여 정보의 다소 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f537-120">hello expected output is quite a bit of information including a list of all hello default rules.</span></span> <span data-ttu-id="4f537-121">hello 다음 예제에서는 hello로 JMESPATH 쿼리 필터를 사용 하 여 hello 기본 규칙 `table` 출력 형식:</span><span class="sxs-lookup"><span data-stu-id="4f537-121">hello following example shows hello default rules using a JMESPATH query filter with hello `table` output format:</span></span>

    ```azurecli
    az network nsg show \
    -g testrg \
    -n nsg-frontend \
    --query 'defaultSecurityRules[].{Access:access,Desc:description,DestPortRange:destinationPortRange,Direction:direction,Priority:priority}' \
    -o table
    ```
   
   <span data-ttu-id="4f537-122">출력:</span><span class="sxs-lookup"><span data-stu-id="4f537-122">Output:</span></span>

        Access    Desc                                                    DestPortRange    Direction      Priority
        
        Allow     Allow inbound traffic from all VMs in VNET              *                Inbound           65000
        Allow     Allow inbound traffic from azure load balancer          *                Inbound           65001
        Deny      Deny all inbound traffic                                *                Inbound           65500
        Allow     Allow outbound traffic from all VMs tooall VMs in VNET  *                Outbound          65000
        Allow     Allow outbound traffic from all VMs tooInternet         *                Outbound          65001
        Deny      Deny all outbound traffic                               *                Outbound          65500



3. <span data-ttu-id="4f537-123">Hello로 hello 인터넷에서에서 액세스 tooport 3389 (RDP)를 허용 하는 규칙을 만들 [az 네트워크 nsg 규칙 만들기](/cli/azure/network/nsg/rule#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="4f537-123">Create a rule that allows access tooport 3389 (RDP) from hello Internet with hello [az network nsg rule create](/cli/azure/network/nsg/rule#create) command.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4f537-124">사용 하는 hello 셸 따라 toomodify hello를 할 수 있습니다 `*` hello 인수를 실행 하기 전에 되지 않으므로 tooexpand hello 인수 뒤에 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="4f537-124">Depending on hello shell you are using, you might need toomodify hello `*` character in hello arguments following so as not tooexpand hello argument before execution.</span></span>
   
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
   
    <span data-ttu-id="4f537-125">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="4f537-125">Expected output:</span></span>
   
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

    <span data-ttu-id="4f537-126">매개 변수</span><span class="sxs-lookup"><span data-stu-id="4f537-126">Parameters:</span></span>

    * <span data-ttu-id="4f537-127">`--resource-group testrg`: 리소스 그룹 toouse hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f537-127">`--resource-group testrg`: hello resource group toouse.</span></span> <span data-ttu-id="4f537-128">대/소문자를 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4f537-128">Note that it is case-insensitive.</span></span>
    * <span data-ttu-id="4f537-129">`--nsg-name NSG-FrontEnd`: Hello NSG는 hello 규칙이 만들어질의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4f537-129">`--nsg-name NSG-FrontEnd`: Name of hello NSG in which hello rule is created.</span></span>
    * <span data-ttu-id="4f537-130">`--name rdp-rule`: Hello 새 규칙의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4f537-130">`--name rdp-rule`: Name for hello new rule.</span></span>
    * <span data-ttu-id="4f537-131">`--access Allow`: Hello 규칙 (Deny 또는 허용)에 대 한 액세스 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="4f537-131">`--access Allow`: Access level for hello rule (Deny or Allow).</span></span>
    * <span data-ttu-id="4f537-132">`--protocol Tcp`: 프로토콜(Tcp, Udp 또는 *)입니다.</span><span class="sxs-lookup"><span data-stu-id="4f537-132">`--protocol Tcp`: Protocol (Tcp, Udp, or *).</span></span>
    * <span data-ttu-id="4f537-133">`--direction Inbound`: Hello 연결 (인바운드 또는 아웃 바운드)의 방향입니다.</span><span class="sxs-lookup"><span data-stu-id="4f537-133">`--direction Inbound`: Direction of hello connection (Inbound or Outbound).</span></span>
    * <span data-ttu-id="4f537-134">`--priority 100`: Hello 규칙에 대 한 우선 순위입니다.</span><span class="sxs-lookup"><span data-stu-id="4f537-134">`--priority 100`: Priority for hello rule.</span></span>
    * <span data-ttu-id="4f537-135">`--source-address-prefix Internet`: CIDR 또는 기본 태그를 사용하는 원본 주소 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="4f537-135">`--source-address-prefix Internet`: Source address prefix in CIDR or using default tags.</span></span>
    * <span data-ttu-id="4f537-136">`--source-port-range "*"`: 원본 포트 또는 포트 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="4f537-136">`--source-port-range "*"`: Source port or port range.</span></span> <span data-ttu-id="4f537-137">포트 연결을 hello 연입니다.</span><span class="sxs-lookup"><span data-stu-id="4f537-137">Port that opened hello connection.</span></span>
    * <span data-ttu-id="4f537-138">`--destination-address-prefix "*"`: CIDR 또는 기본 태그를 사용하는 대상 주소 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="4f537-138">`--destination-address-prefix "*"`: Destination address prefix in CIDR or using default tags.</span></span>
    * <span data-ttu-id="4f537-139">`--destination-port-range 3389`: 대상 포트 또는 포트 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="4f537-139">`--destination-port-range 3389`: Destination port or port range.</span></span> <span data-ttu-id="4f537-140">Hello 연결 요청을 수신 하는 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="4f537-140">Port that receives hello connection request.</span></span>



4. <span data-ttu-id="4f537-141">Hello 인터넷에서에서 액세스 tooport 80 (HTTP)를 허용 하는 규칙을 만들 **az 네트워크 nsg 규칙 만들기** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="4f537-141">Create a rule that allows access tooport 80 (HTTP) from hello Internet **az network nsg rule create** command.</span></span>
   
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
   
    <span data-ttu-id="4f537-142">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="4f537-142">Expected putput:</span></span>
   
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

5. <span data-ttu-id="4f537-143">Hello NSG toohello 바인딩 **프런트 엔드** hello로 서브넷 [az 네트워크 vnet 서브넷 업데이트](/cli/azure/network/vnet/subnet#update) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="4f537-143">Bind hello NSG toohello **FrontEnd** subnet with hello [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) command.</span></span>
        
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name FrontEnd \
    --resource-group testrg \
    --network-security-group NSG-FrontEnd
    ```
   
    <span data-ttu-id="4f537-144">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="4f537-144">Expected output:</span></span>
   
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

## <a name="create-hello-nsg-for-hello-backend-subnet"></a><span data-ttu-id="4f537-145">Hello에 대 한 hello NSG 만들기 `BackEnd` 서브넷</span><span class="sxs-lookup"><span data-stu-id="4f537-145">Create hello NSG for hello `BackEnd` subnet</span></span>
<span data-ttu-id="4f537-146">명명 된 NSG toocreate *NSG 백 엔드* hello 단계 다음에 따라 이전 hello 시나리오에 따라, 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f537-146">toocreate an NSG named *NSG-BackEnd* based on hello scenario preceding, follow hello steps following.</span></span>

1. <span data-ttu-id="4f537-147">Hello 만들기 `NSG-BackEnd` 와 NSG **az 네트워크 nsg 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="4f537-147">Create hello `NSG-BackEnd` NSG with **az network nsg create**.</span></span>
   
    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-BackEnd \
    --location centralus
    ```
   
    <span data-ttu-id="4f537-148">앞, 2 단계에서 설명한 대로 hello 출력은 매우 클 기본 규칙을 포함 하 여 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f537-148">As in step 2, preceding, hello expected output is quite large, including default rules.</span></span>
   
2. <span data-ttu-id="4f537-149">액세스 tooport 1433 (SQL) hello에서 허용 하는 규칙을 만들 `FrontEnd` hello로 서브넷 **az 네트워크 nsg 규칙 만들기** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="4f537-149">Create a rule that allows access tooport 1433 (SQL) from hello `FrontEnd` subnet with hello **az network nsg rule create** command.</span></span>
   
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
   
    <span data-ttu-id="4f537-150">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="4f537-150">Expected output:</span></span>

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

3. <span data-ttu-id="4f537-151">사용 하 여 액세스 toohello 인터넷 거부 하는 규칙을 만들 hello **az 네트워크 nsg 규칙 만들기** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="4f537-151">Create a rule that denies access toohello Internet using hello **az network nsg rule create** command.</span></span>
   
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
   
    <span data-ttu-id="4f537-152">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="4f537-152">Expected putput:</span></span>
   
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

4. <span data-ttu-id="4f537-153">Hello NSG toohello 바인딩 `BackEnd` hello를 사용 하 여 서브넷 **az 네트워크 vnet 서브넷 집합** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="4f537-153">Bind hello NSG toohello `BackEnd` subnet using hello **az network vnet subnet set** command.</span></span>
   
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name BackEnd \
    --resource-group testrg \
    --network-security-group NSG-BackEnd
    ```
   
    <span data-ttu-id="4f537-154">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="4f537-154">Expected output:</span></span>
   
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
