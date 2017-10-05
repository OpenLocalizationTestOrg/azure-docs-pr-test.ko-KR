---
title: "네트워크 보안 그룹 관리 - Azure CLI 1.0 | Microsoft Docs"
description: "Azure CLI(명령줄 인터페이스) 1.0을 사용하여 네트워크 보안 그룹을 관리하는 방법에 대해 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2e53c3ff2ffbef95d6b72ca6afb3b4de377f0389
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-network-security-groups-using-the-azure-cli-10"></a><span data-ttu-id="91eb7-103">Azure CLI 1.0을 사용하여 네트워크 보안 그룹 관리</span><span class="sxs-lookup"><span data-stu-id="91eb7-103">Manage network security groups using the Azure CLI 1.0</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="91eb7-104">태스크를 완료하기 위한 CLI 버전</span><span class="sxs-lookup"><span data-stu-id="91eb7-104">CLI versions to complete the task</span></span> 

<span data-ttu-id="91eb7-105">다음 CLI 버전 중 하나를 사용하여 태스크를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91eb7-105">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="91eb7-106">[Azure CLI 1.0](#View-existing-NSGs) - 클래식 및 리소스 관리 배포 모델용 CLI</span><span class="sxs-lookup"><span data-stu-id="91eb7-106">[Azure CLI 1.0](#View-existing-NSGs) – our CLI for the classic and resource management deployment models</span></span> 
- <span data-ttu-id="91eb7-107">[Azure CLI 2.0](virtual-network-manage-nsg-arm-cli.md) - 리소스 관리 배포 모델용 차세대 CLI(이 문서)</span><span class="sxs-lookup"><span data-stu-id="91eb7-107">[Azure CLI 2.0](virtual-network-manage-nsg-arm-cli.md) - our next generation CLI for the resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="91eb7-108">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91eb7-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="91eb7-109">이 문서에서는 Resource Manager 배포 모델 사용을 설명하며 Microsoft에서는 대부분의 새로운 배포에 대해 클래식 배포 모델 대신 이 모델을 사용하도록 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="91eb7-109">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="91eb7-110">정보 검색</span><span class="sxs-lookup"><span data-stu-id="91eb7-110">Retrieve Information</span></span>
<span data-ttu-id="91eb7-111">기존 NSG를 보고 기존 NSG에 대한 규칙을 검색하며 NSG가 연결된 리소스에 대해 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91eb7-111">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="91eb7-112">기존 NSG 보기</span><span class="sxs-lookup"><span data-stu-id="91eb7-112">View existing NSGs</span></span>
<span data-ttu-id="91eb7-113">특정 리소스 그룹에 있는 NSG 목록을 보려면 아래와 같이 `azure network nsg list` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="91eb7-113">To view the list of NSGs in a specific resource group, run the `azure network nsg list` command as shown below.</span></span>

```azurecli
azure network nsg list --resource-group RG-NSG
```

<span data-ttu-id="91eb7-114">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="91eb7-114">Expected output:</span></span>

    info:    Executing command network nsg list
    + Getting the network security groups
    data:    Name          Location
    data:    ------------  --------
    data:    NSG-BackEnd   westus
    data:    NSG-FrontEnd  westus
    info:    network nsg list command OK

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="91eb7-115">NSG에 대한 모든 규칙 나열</span><span class="sxs-lookup"><span data-stu-id="91eb7-115">List all rules for an NSG</span></span>
<span data-ttu-id="91eb7-116">**NSG-FrontEnd**로 명명된 NSG의 규칙을 보려면 아래와 같이 `azure network nsg show` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="91eb7-116">To view the rules of an NSG named **NSG-FrontEnd**, run the `azure network nsg show` command as shown below.</span></span> 

```azurecli
azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd
```

<span data-ttu-id="91eb7-117">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="91eb7-117">Expected output:</span></span>

    info:    Executing command network nsg show
    + Looking up the network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    data:    Name                            : NSG-FrontEnd
    data:    Type                            : Microsoft.Network/networkSecurityGroups
    data:    Location                        : westus
    data:    Provisioning state              : Succeeded
    data:    Tags                            : displayName=NSG - Front End
    data:    Security group rules:
    data:    Name                           Source IP          Source Port  Destination IP  Destination Port  Protocol  Direction  Access  Priority
    data:    -----------------------------  -----------------  -----------  --------------  ----------------  --------  ---------  ------  --------
    data:    rdp-rule                       Internet           *            *               3389              Tcp       Inbound    Allow   100
    data:    web-rule                       Internet           *            *               80                Tcp       Inbound    Allow   101
    data:    AllowVnetInBound               VirtualNetwork     *            VirtualNetwork  *                 *         Inbound    Allow   65000
    data:    AllowAzureLoadBalancerInBound  AzureLoadBalancer  *            *               *                 *         Inbound    Allow   65001
    data:    DenyAllInBound                 *                  *            *               *                 *         Inbound    Deny    65500
    data:    AllowVnetOutBound              VirtualNetwork     *            VirtualNetwork  *                 *         Outbound   Allow   65000
    data:    AllowInternetOutBound          *                  *            Internet        *                 *         Outbound   Allow   65001
    data:    DenyAllOutBound                *                  *            *               *                 *         Outbound   Deny    65500
    info:    network nsg show command OK

> [!NOTE]
> <span data-ttu-id="91eb7-118">또한 `azure network nsg rule list --resource-group RG-NSG --nsg-name NSG-FrontEnd`을 사용하여 **NSG-FrontEnd** NSG에서 규칙을 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91eb7-118">You can also use `azure network nsg rule list --resource-group RG-NSG --nsg-name NSG-FrontEnd` to list the rules from the **NSG-FrontEnd** NSG.</span></span>
>

### <a name="view-nsg-associations"></a><span data-ttu-id="91eb7-119">NSG 연결 보기</span><span class="sxs-lookup"><span data-stu-id="91eb7-119">View NSG associations</span></span>

<span data-ttu-id="91eb7-120">**NSG-FrontEnd** NSG가 연결된 리소스를 보려면 아래와 같이 `azure network nsg show` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="91eb7-120">To view what resources the **NSG-FrontEnd** NSG is associate with, run the `azure network nsg show` command as shown below.</span></span> <span data-ttu-id="91eb7-121">유일한 차이점은 **--json** 매개 변수를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="91eb7-121">Notice that the only difference is the use of the **--json** parameter.</span></span>

```azurecli
azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json
```

<span data-ttu-id="91eb7-122">아래와 같이 **NetworkInterfaces** 및 **서브넷** 속성을 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="91eb7-122">Look for the **networkInterfaces** and **subnets** properties as shown below:</span></span>

    "networkInterfaces": [],
    ...
    "subnets": [
        {
            "id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
        }
    ],
    ...

<span data-ttu-id="91eb7-123">위의 예에서 NSG는 NIC(네트워크 인터페이스)에 연결되지 않고 **FrontEnd**라는 서브넷에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="91eb7-123">In the example above, the NSG is not associated to any network interfaces (NICs), and it is associated to a subnet named **FrontEnd**.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="91eb7-124">규칙 관리</span><span class="sxs-lookup"><span data-stu-id="91eb7-124">Manage rules</span></span>
<span data-ttu-id="91eb7-125">기존 NSG에 규칙을 추가하고 기존 규칙을 편집하며 규칙을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91eb7-125">You can add rules to an existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="91eb7-126">규칙 추가</span><span class="sxs-lookup"><span data-stu-id="91eb7-126">Add a rule</span></span>
<span data-ttu-id="91eb7-127">컴퓨터에서 **NSG-FrontEnd** NSG에 포트 **443**에 대한 **인바운드** 트래픽을 허용하는 규칙을 추가하려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="91eb7-127">To add a rule allowing **inbound** traffic to port **443** from any machine to the **NSG-FrontEnd** NSG, enter the following command:</span></span>

```azurecli
azure network nsg rule create --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --description "Allow access to port 443 for HTTPS" \
    --protocol Tcp \
    --source-address-prefix * \
    --source-port-range * \
    --destination-address-prefix * \
    --destination-port-range 443 \
    --access Allow \
    --priority 102 \
    --direction Inbound
```

<span data-ttu-id="91eb7-128">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="91eb7-128">Expected output:</span></span>

    info:    Executing command network nsg rule create
    + Looking up the network security rule "allow-https"
    + Creating a network security rule "allow-https"
    + Looking up the network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https
    data:    Name                            : allow-https
    data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
    data:    Provisioning state              : Succeeded
    data:    Description                     : Allow access to port 443 for HTTPS
    data:    Source IP                       : *
    data:    Source Port                     : *
    data:    Destination IP                  : *
    data:    Destination Port                : 443
    data:    Protocol                        : Tcp
    data:    Direction                       : Inbound
    data:    Access                          : Allow
    data:    Priority                        : 102
    info:    network nsg rule create command OK

### <a name="change-a-rule"></a><span data-ttu-id="91eb7-129">규칙 변경</span><span class="sxs-lookup"><span data-stu-id="91eb7-129">Change a rule</span></span>
<span data-ttu-id="91eb7-130">**인터넷**에서 인바운드 트래픽을 허용하도록 위에서 만든 규칙을 변경하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="91eb7-130">To change the rule created above to allow inbound traffic from the **Internet** only, run the following command:</span></span>

```azurecli
azure network nsg rule set --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --source-address-prefix Internet
```

<span data-ttu-id="91eb7-131">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="91eb7-131">Expected output:</span></span>

    info:    Executing command network nsg rule set
    + Looking up the network security group "NSG-FrontEnd"
    + Setting a network security rule "allow-https"
    + Looking up the network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https
    data:    Name                            : allow-https
    data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
    data:    Provisioning state              : Succeeded
    data:    Description                     : Allow access to port 443 for HTTPS
    data:    Source IP                       : Internet
    data:    Source Port                     : *
    data:    Destination IP                  : *
    data:    Destination Port                : 443
    data:    Protocol                        : Tcp
    data:    Direction                       : Inbound
    data:    Access                          : Allow
    data:    Priority                        : 102
    info:    network nsg rule set command OK

### <a name="delete-a-rule"></a><span data-ttu-id="91eb7-132">규칙 삭제</span><span class="sxs-lookup"><span data-stu-id="91eb7-132">Delete a rule</span></span>
<span data-ttu-id="91eb7-133">위에서 만든 규칙을 삭제하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="91eb7-133">To delete the rule created above, run the following command:</span></span>

```azurecli
azure network nsg rule delete --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --quiet
```

> [!NOTE]
> <span data-ttu-id="91eb7-134">`--quiet` 매개 변수를 사용하면 삭제를 확인하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91eb7-134">The `--quiet` parameter ensures you don't need to confirm the deletion.</span></span>
>

<span data-ttu-id="91eb7-135">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="91eb7-135">Expected output:</span></span>

    info:    Executing command network nsg rule delete
    + Looking up the network security group "NSG-FrontEnd"
    + Deleting network security rule "allow-https"
    info:    network nsg rule delete command OK

## <a name="manage-associations"></a><span data-ttu-id="91eb7-136">연결 관리</span><span class="sxs-lookup"><span data-stu-id="91eb7-136">Manage associations</span></span>
<span data-ttu-id="91eb7-137">NSG를 서브넷 및 NIC에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91eb7-137">You can associate an NSG to subnets and NICs.</span></span> <span data-ttu-id="91eb7-138">또한 연결된 모든 리소스에서 NSG를 분리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91eb7-138">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-to-a-nic"></a><span data-ttu-id="91eb7-139">NIC에 NSG 연결</span><span class="sxs-lookup"><span data-stu-id="91eb7-139">Associate an NSG to a NIC</span></span>
<span data-ttu-id="91eb7-140">**NSG-FrontEnd** NSG를 **TestNICWeb1** NIC에 연결하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="91eb7-140">To associate the **NSG-FrontEnd** NSG to the **TestNICWeb1** NIC, run the following command:</span></span>

```azurecli
azure network nic set --resource-group RG-NSG \
    --name TestNICWeb1 \
    --network-security-group-name NSG-FrontEnd
```

<span data-ttu-id="91eb7-141">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="91eb7-141">Expected output:</span></span>

    info:    Executing command network nic set
    + Looking up the network interface "TestNICWeb1"
    + Looking up the network security group "NSG-FrontEnd"
    + Updating network interface "TestNICWeb1"
    + Looking up the network interface "TestNICWeb1"
    data:    Id                              : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1
    data:    Name                            : TestNICWeb1
    data:    Type                            : Microsoft.Network/networkInterfaces
    data:    Location                        : westus
    data:    Provisioning state              : Succeeded
    data:    MAC address                     : 00-0D-3A-30-A1-F8
    data:    Enable IP forwarding            : false
    data:    Tags                            : displayName=NetworkInterfaces - Web
    data:    Network security group          : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    data:    Virtual machine                 : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Compute/virtualMachines/Web1
    data:    IP configurations:
    data:      Name                          : ipconfig1
    data:      Provisioning state            : Succeeded
    data:      Public IP address             : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/publicIPAddresses/TestPIPWeb1
    data:      Private IP address            : 192.168.1.5
    data:      Private IP Allocation Method  : Dynamic
    data:      Subnet                        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:
    info:    network nic set command OK

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="91eb7-142">NIC에서 NSG 분리</span><span class="sxs-lookup"><span data-stu-id="91eb7-142">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="91eb7-143">**NSG-FrontEnd** NSG를 **TestNICWeb1** NIC에서 분리하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="91eb7-143">To dissociate the **NSG-FrontEnd** NSG from the **TestNICWeb1** NIC, run the following command:</span></span>

```azurecli
azure network nic set --resource-group RG-NSG --name TestNICWeb1 --network-security-group-id ""
```

> [!NOTE]
> <span data-ttu-id="91eb7-144">`network-security-group-id` 매개 변수에 대한 ""(비어 있음) 값에 유의합니다.</span><span class="sxs-lookup"><span data-stu-id="91eb7-144">Notice the "" (empty) value for the `network-security-group-id` parameter.</span></span> <span data-ttu-id="91eb7-145">NSG에 대한 연결을 제거하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="91eb7-145">That is how you remove an association to an NSG.</span></span> <span data-ttu-id="91eb7-146">`network-security-group-name` 매개 변수로 동일하게 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="91eb7-146">You can't do the same with the `network-security-group-name` parameter.</span></span>
> 

<span data-ttu-id="91eb7-147">예상된 결과:</span><span class="sxs-lookup"><span data-stu-id="91eb7-147">Expected result:</span></span>

    info:    Executing command network nic set
    + Looking up the network interface "TestNICWeb1"
    + Updating network interface "TestNICWeb1"
    + Looking up the network interface "TestNICWeb1"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1
    data:    Name                            : TestNICWeb1
    data:    Type                            : Microsoft.Network/networkInterfaces
    data:    Location                        : westus
    data:    Provisioning state              : Succeeded
    data:    MAC address                     : 00-0D-3A-30-A1-F8
    data:    Enable IP forwarding            : false
    data:    Tags                            : displayName=NetworkInterfaces - Web
    data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Compute/virtualMachines/Web1
    data:    IP configurations:
    data:      Name                          : ipconfig1
    data:      Provisioning state            : Succeeded
    data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/publicIPAddresses/TestPIPWeb1
    data:      Private IP address            : 192.168.1.5
    data:      Private IP Allocation Method  : Dynamic
    data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:
    info:    network nic set command OK

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="91eb7-148">서브넷에서 NSG 분리</span><span class="sxs-lookup"><span data-stu-id="91eb7-148">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="91eb7-149">**NSG-FrontEnd** NSG를 **FrontEnd** 서브넷에서 분리하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="91eb7-149">To dissociate the **NSG-FrontEnd** NSG from the **FrontEnd** subnet, run the following command:</span></span>

```azurecli
azure network vnet subnet set --resource-group RG-NSG \
    --vnet-name TestVNet \
    --name FrontEnd \
    --network-security-group-id ""
```

<span data-ttu-id="91eb7-150">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="91eb7-150">Expected output:</span></span>

    info:    Executing command network vnet subnet set
    + Looking up the subnet "FrontEnd"
    + Setting subnet "FrontEnd"
    + Looking up the subnet "FrontEnd"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:    Type                            : Microsoft.Network/virtualNetworks/subnets
    data:    ProvisioningState               : Succeeded
    data:    Name                            : FrontEnd
    data:    Address prefix                  : 192.168.1.0/24
    data:    IP configurations:
    data:      /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1
    data:      /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1
    data:
    info:    network vnet subnet set command OK

### <a name="associate-an-nsg-to-a-subnet"></a><span data-ttu-id="91eb7-151">서브넷에 NSG 연결</span><span class="sxs-lookup"><span data-stu-id="91eb7-151">Associate an NSG to a subnet</span></span>
<span data-ttu-id="91eb7-152">**NSG-FrontEnd** NSG를 **FrontEnd** 서브넷에 다시 연결하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="91eb7-152">To associate the **NSG-FrontEnd** NSG to the **FronEnd** subnet again, run the following command:</span></span>

```azurecli
azure network vnet subnet set --resource-group RG-NSG \
    --vnet-name TestVNet \
    --name FrontEnd \
    --network-security-group-name NSG-FronEnd
```

> [!NOTE]
> <span data-ttu-id="91eb7-153">**NSG-FrontEnd** NSG가 **TestVNet** 가상 네트워크와 동일한 리소스 그룹에 있는 경우 위의 명령이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="91eb7-153">The command above only works because the **NSG-FrontEnd** NSG is in the same resource group as the virtual network **TestVNet**.</span></span> <span data-ttu-id="91eb7-154">NSG가 다른 리소스 그룹에 있으면 대신 `--network-security-group-id` 매개 변수를 사용하고 NSG에 대한 전체 ID를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91eb7-154">If the NSG is in a different resource group, you need to use the `--network-security-group-id` parameter instead, and provide the full id for the NSG.</span></span> <span data-ttu-id="91eb7-155">`azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json`을 실행하며 **id** 속성을 찾아 보아 id를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91eb7-155">You can retrieve the id by running `azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json` and looking for the **id** property.</span></span> 
> 

<span data-ttu-id="91eb7-156">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="91eb7-156">Expected output:</span></span>

        info:    Executing command network vnet subnet set
        + Looking up the subnet "FrontEnd"
        + Looking up the network security group "NSG-FrontEnd"
        + Setting subnet "FrontEnd"
        + Looking up the subnet "FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:    Network security group          : [object Object]
        data:    IP configurations:
        data:      /subscriptions/[Subscription Id]resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1
        data:      /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1
        data:
        info:    network vnet subnet set command OK

## <a name="delete-an-nsg"></a><span data-ttu-id="91eb7-157">NSG 삭제</span><span class="sxs-lookup"><span data-stu-id="91eb7-157">Delete an NSG</span></span>
<span data-ttu-id="91eb7-158">리소스에 연결되지 않은 경우 NSG를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91eb7-158">You can only delete an NSG if it's not associated to any resource.</span></span> <span data-ttu-id="91eb7-159">NSG를 삭제하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="91eb7-159">To delete an NSG, follow the steps below.</span></span>

1. <span data-ttu-id="91eb7-160">NSG에 연결된 리소스를 확인하려면 [NSG 연결 보기](#View-NSGs-associations)에서처럼 `azure network nsg show`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="91eb7-160">To check the resources associated to an NSG, run the `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="91eb7-161">NSG가 NIC에 연결된 경우 각 NIC에 대한 [NIC에서 NSG 분리](#Dissociate-an-NSG-from-a-NIC)에서처럼 `azure network nic set`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="91eb7-161">If the NSG is associated to any NICs, run the `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="91eb7-162">NSG가 서브넷에 연결된 경우 각 서브넷에 대한 [서브넷에서 NSG 분리](#Dissociate-an-NSG-from-a-subnet)에서처럼 `azure network vnet subnet set`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="91eb7-162">If the NSG is associated to any subnet, run the `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="91eb7-163">NSG를 삭제하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="91eb7-163">To delete the NSG, run the following command:</span></span>

    ```azurecli
    azure network nsg delete --resource-group RG-NSG --name NSG-FrontEnd --quiet
    ```

    <span data-ttu-id="91eb7-164">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="91eb7-164">Expected output:</span></span>

        info:    Executing command network nsg delete
        + Looking up the network security group "NSG-FrontEnd"
        + Deleting network security group "NSG-FrontEnd"
        info:    network nsg delete command OK

## <a name="next-steps"></a><span data-ttu-id="91eb7-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="91eb7-165">Next steps</span></span>
* <span data-ttu-id="91eb7-166">[로깅을 사용합니다](virtual-network-nsg-manage-log.md) .</span><span class="sxs-lookup"><span data-stu-id="91eb7-166">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

