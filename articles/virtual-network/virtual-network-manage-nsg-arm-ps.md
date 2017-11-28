---
title: "네트워크 보안 그룹 관리 - Azure PowerShell | Microsoft Docs"
description: "PowerShell을 사용하여 네트워크 보안 그룹을 관리하는 방법을 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3706ce6c-d9ae-46cb-a048-f0a4e84dc5cc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ca7f4926ca4edf9d20612aca74f6ae5f0ed847b3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-network-security-groups-using-powershell"></a><span data-ttu-id="e7aa7-103">PowerShell을 사용하여 네트워크 보안 그룹 관리</span><span class="sxs-lookup"><span data-stu-id="e7aa7-103">Manage network security groups using PowerShell</span></span>

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="e7aa7-104">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e7aa7-105">이 문서에서는 Resource Manager 배포 모델 사용을 설명하며 Microsoft에서는 대부분의 새로운 배포에 대해 클래식 배포 모델 대신 이 모델을 사용하도록 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-105">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="e7aa7-106">정보 검색</span><span class="sxs-lookup"><span data-stu-id="e7aa7-106">Retrieve Information</span></span>
<span data-ttu-id="e7aa7-107">기존 NSG를 보고 기존 NSG에 대한 규칙을 검색하며 NSG가 연결된 리소스에 대해 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-107">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="e7aa7-108">기존 NSG 보기</span><span class="sxs-lookup"><span data-stu-id="e7aa7-108">View existing NSGs</span></span>
<span data-ttu-id="e7aa7-109">구독에서 모든 기존 NSG를 보려면 `Get-AzureRmNetworkSecurityGroup` cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-109">To view all existing NSGs in a subscription, run the `Get-AzureRmNetworkSecurityGroup` cmdlet.</span></span>

<span data-ttu-id="e7aa7-110">예상된 결과:</span><span class="sxs-lookup"><span data-stu-id="e7aa7-110">Expected result:</span></span>

    Name                 : NSG-BackEnd
    ResourceGroupName    : RG-NSG
    Location             : westus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-BackEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 :                            
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : NSG-FrontEnd
    ResourceGroupName    : RG-NSG
    Location             : eastus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/NRP-RG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : WEB1
    ResourceGroupName    : RG101
    Location             : eastus2
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG101/providers/M
                           icrosoft.Network/networkSecurityGroups/WEB1
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]


<span data-ttu-id="e7aa7-111">특정 리소스 그룹에 있는 NSG 목록을 보려면 `Get-AzureRmNetworkSecurityGroup` cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-111">To view the list of NSGs in a specific resource group, run the `Get-AzureRmNetworkSecurityGroup` cmdlet.</span></span>

<span data-ttu-id="e7aa7-112">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="e7aa7-112">Expected output:</span></span>

    Name                 : NSG-BackEnd
    ResourceGroupName    : RG-NSG
    Location             : westus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-BackEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 :                            
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : NSG-FrontEnd
    ResourceGroupName    : RG-NSG
    Location             : eastus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/NRP-RG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="e7aa7-113">NSG에 대한 모든 규칙 나열</span><span class="sxs-lookup"><span data-stu-id="e7aa7-113">List all rules for an NSG</span></span>
<span data-ttu-id="e7aa7-114">**NSG-FrontEnd**로 명명된 NSG의 규칙을 보려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-114">To view the rules of an NSG named **NSG-FrontEnd**, enter the following command:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd | Select SecurityRules -ExpandProperty SecurityRules
```

<span data-ttu-id="e7aa7-115">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="e7aa7-115">Expected output:</span></span>

    Name                     : rdp-rule
    Id                       : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule
    Etag                     : W/"[Id]"
    ProvisioningState        : Succeeded
    Description              : Allow RDP
    Protocol                 : Tcp
    SourcePortRange          : *
    DestinationPortRange     : 3389
    SourceAddressPrefix      : Internet
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 100
    Direction                : Inbound

    Name                     : web-rule
    Id                       : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule
    Etag                     : W/"[Id]"
    ProvisioningState        : Succeeded
    Description              : Allow HTTP
    Protocol                 : Tcp
    SourcePortRange          : *
    DestinationPortRange     : 80
    SourceAddressPrefix      : Internet
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 101
    Direction                : Inbound

> [!NOTE]
> <span data-ttu-id="e7aa7-116">또한 `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules`을 사용하여 **NSG-FrontEnd** NSG에서 기본 규칙을 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-116">You can also use `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` to list the default rules from the **NSG-FrontEnd** NSG.</span></span>
> 

### <a name="view-nsgs-associations"></a><span data-ttu-id="e7aa7-117">NSG 연결 보기</span><span class="sxs-lookup"><span data-stu-id="e7aa7-117">View NSGs associations</span></span>
<span data-ttu-id="e7aa7-118">**NSG-FrontEnd** NSG가 연결된 리소스를 보려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-118">To view what resources the **NSG-FrontEnd** NSG is associate with, run the following command:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
```

<span data-ttu-id="e7aa7-119">아래와 같이 **NetworkInterfaces** 및 **서브넷** 속성을 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-119">Look for the **NetworkInterfaces** and **Subnets** properties as shown below:</span></span>

    NetworkInterfaces    : []
    Subnets              : [
                             {
                               "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                               "IpConfigurations": []
                             }
                           ]

<span data-ttu-id="e7aa7-120">이전 예에서 NSG는 NIC(네트워크 인터페이스)에 연결되지 않습니다. **FrontEnd**라는 서브넷에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-120">In the previous example, the NSG is not associated to any network interfaces (NICs); it is associated to a subnet named **FrontEnd**.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="e7aa7-121">규칙 관리</span><span class="sxs-lookup"><span data-stu-id="e7aa7-121">Manage rules</span></span>
<span data-ttu-id="e7aa7-122">기존 NSG에 규칙을 추가하고 기존 규칙을 편집하며 규칙을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-122">You can add rules to an existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="e7aa7-123">규칙 추가</span><span class="sxs-lookup"><span data-stu-id="e7aa7-123">Add a rule</span></span>
<span data-ttu-id="e7aa7-124">컴퓨터에서 **NSG-FrontEnd** NSG에 포트 **443**에 대한 **인바운드** 트래픽을 허용하는 규칙을 추가하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-124">To add a rule allowing **inbound** traffic to port **443** from any machine to the **NSG-FrontEnd** NSG, complete the following steps:</span></span>

1. <span data-ttu-id="e7aa7-125">다음 명령을 실행하여 기존 NSG를 검색하고 변수에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-125">Run the following command to retrieve the existing NSG and store it in a variable:</span></span>

    ```powershell   
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="e7aa7-126">다음 명령을 실행하여 규칙을 NSG에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-126">Run the following command to add a rule to the NSG:</span></span>

    ```powershell
    Add-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
    -Name https-rule `
    -Description "Allow HTTPS" `
    -Access Allow `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 102 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443
    ```

3. <span data-ttu-id="e7aa7-127">NSG에 대한 변경 사항을 저장하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-127">To save the changes made to the NSG, run the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```
    <span data-ttu-id="e7aa7-128">보안 규칙만 표시하는 확장된 출력:</span><span class="sxs-lookup"><span data-stu-id="e7aa7-128">Expected output showing only the security rules:</span></span>
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 },
                                 {
                                   "Name": "https-rule",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/https-rule",
                                   "Description": "Allow HTTPS",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "443",
                                   "SourceAddressPrefix": "*",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 102,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]

### <a name="change-a-rule"></a><span data-ttu-id="e7aa7-129">규칙 변경</span><span class="sxs-lookup"><span data-stu-id="e7aa7-129">Change a rule</span></span>
<span data-ttu-id="e7aa7-130">**인터넷** 에서 인바운드 트래픽을 허용하도록 위에서 만든 규칙을 변경하려면는 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-130">To change the rule created above to allow inbound traffic from the **Internet** only, follow the steps below.</span></span>

1. <span data-ttu-id="e7aa7-131">다음 명령을 실행하여 기존 NSG를 검색하고 변수에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-131">Run the following command to retrieve the existing NSG and store it in a variable:</span></span>

    ```powershell 
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="e7aa7-132">새 규칙 설정을 사용하여 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-132">Run the following command with the new rule settings:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
    -Name https-rule `
    -Description "Allow HTTPS" `
    -Access Allow `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 102 `
    -SourceAddressPrefix Internet `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443
    ```

3. <span data-ttu-id="e7aa7-133">NSG에 대한 변경 사항을 저장하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-133">To save the changes made to the NSG, run the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="e7aa7-134">보안 규칙만 표시하는 확장된 출력:</span><span class="sxs-lookup"><span data-stu-id="e7aa7-134">Expected output showing only the security rules:</span></span>
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 },
                                 {
                                   "Name": "https-rule",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/https-rule",
                                   "Description": "Allow HTTPS",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "443",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 102,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]

### <a name="delete-a-rule"></a><span data-ttu-id="e7aa7-135">규칙 삭제</span><span class="sxs-lookup"><span data-stu-id="e7aa7-135">Delete a rule</span></span>
1. <span data-ttu-id="e7aa7-136">다음 명령을 실행하여 기존 NSG를 검색하고 변수에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-136">Run the following command to retrieve the existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="e7aa7-137">NSG로부터 규칙을 삭제하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-137">Run the following command to remove the rule from the NSG:</span></span>

    ```powershell
    Remove-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg -Name https-rule
    ```

3. <span data-ttu-id="e7aa7-138">NSG에 대한 변경 사항을 저장하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-138">Save the changes made to the NSG, by running the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="e7aa7-139">보안 규칙만 표시하는 예상된 출력에는 더 이상 **https-rule** 이 나열되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-139">Expected output showing only the security rules, notice the **https-rule** is no longer listed:</span></span>
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 }
                               ]

## <a name="manage-associations"></a><span data-ttu-id="e7aa7-140">연결 관리</span><span class="sxs-lookup"><span data-stu-id="e7aa7-140">Manage associations</span></span>
<span data-ttu-id="e7aa7-141">NSG를 서브넷 및 NIC에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-141">You can associate an NSG to subnets and NICs.</span></span> <span data-ttu-id="e7aa7-142">또한 연결된 모든 리소스에서 NSG를 분리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-142">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-to-a-nic"></a><span data-ttu-id="e7aa7-143">NIC에 NSG 연결</span><span class="sxs-lookup"><span data-stu-id="e7aa7-143">Associate an NSG to a NIC</span></span>
<span data-ttu-id="e7aa7-144">**NSG-FrontEnd** NSG를 **TestNICWeb1** NIC에 연결하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-144">To associate the **NSG-FrontEnd** NSG to the **TestNICWeb1** NIC, complete the following steps:</span></span>

1. <span data-ttu-id="e7aa7-145">다음 명령을 실행하여 기존 NSG를 검색하고 변수에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-145">Run the following command to retrieve the existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="e7aa7-146">다음 명령을 실행하여 기존 NIC를 검색하고 변수에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-146">Run the following command to retrieve the existing NIC and store it in a variable:</span></span>

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

3. <span data-ttu-id="e7aa7-147">**NIC** 변수의 **NetworkSecurityGroup** 속성을 다음 명령을 입력하여 **NSG** 변수의 값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-147">Set the **NetworkSecurityGroup** property of the **NIC** variable to the value of the **NSG** variable, by entering the following command:</span></span>

    ```powershell
    $nic.NetworkSecurityGroup = $nsg
    ```

4. <span data-ttu-id="e7aa7-148">NIC에 대한 변경 사항을 저장하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-148">To save the changes made to the NIC, run the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    <span data-ttu-id="e7aa7-149">**NetworkSecurityGroup** 속성만을 표시하는 예상된 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-149">Expected output showing only the **NetworkSecurityGroup** property:</span></span>
   
        NetworkSecurityGroup : {
                                 "SecurityRules": [],
                                 "DefaultSecurityRules": [],
                                 "NetworkInterfaces": [],
                                 "Subnets": [],
                                 "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                               }

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="e7aa7-150">NIC에서 NSG 분리</span><span class="sxs-lookup"><span data-stu-id="e7aa7-150">Dissociate an NSG from a NIC</span></span>
<span data-ttu-id="e7aa7-151">**NSG-FrontEnd** NSG를 **TestNICWeb1** NIC에서 분리하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-151">To dissociate the **NSG-FrontEnd** NSG from the **TestNICWeb1** NIC, complete the following steps:</span></span>

1. <span data-ttu-id="e7aa7-152">다음 명령을 실행하여 기존 NIC를 검색하고 변수에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-152">Run the following command to retrieve the existing NIC and store it in a variable:</span></span>

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

2. <span data-ttu-id="e7aa7-153">**NIC** 변수의 **NetworkSecurityGroup** 속성을 다음 명령을 실행하여 **$null** 변수의 값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-153">Set the **NetworkSecurityGroup** property of the **NIC** variable to **$null** by running the following command:</span></span>

    ```powershell
    $nic.NetworkSecurityGroup = $null
    ```

3. <span data-ttu-id="e7aa7-154">NIC에 대한 변경 사항을 저장하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-154">To save the changes made to the NIC, run the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    <span data-ttu-id="e7aa7-155">**NetworkSecurityGroup** 속성만을 표시하는 예상된 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-155">Expected output showing only the **NetworkSecurityGroup** property:</span></span>
   
        NetworkSecurityGroup : null

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="e7aa7-156">서브넷에서 NSG 분리</span><span class="sxs-lookup"><span data-stu-id="e7aa7-156">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="e7aa7-157">**NSG-FrontEnd** NSG를 **FrontEnd** 서브넷에서 분리하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-157">To dissociate the **NSG-FrontEnd** NSG from the **FrontEnd** subnet, complete the following steps:</span></span>

1. <span data-ttu-id="e7aa7-158">다음 명령을 실행하여 기존 VNet 을 검색하고 변수에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-158">Run the following command to retrieve the existing VNet and store it in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. <span data-ttu-id="e7aa7-159">다음 명령을 실행하여 **FrontEnd** 서브넷을 검색하고 변수에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-159">Run the following command to retrieve the **FrontEnd** subnet and store it in a variable:</span></span>

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. <span data-ttu-id="e7aa7-160">**서브넷** 변수의 **NetworkSecurityGroup** 속성을 다음 명령을 입력하여 **$null** 변수의 값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-160">Set the **NetworkSecurityGroup** property of the **subnet** variable to **$null** by entering the following command:</span></span>

    ```powershell
    $subnet.NetworkSecurityGroup = $null
    ```

4. <span data-ttu-id="e7aa7-161">서브넷에 대한 변경 사항을 저장하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-161">To save the changes made to the subnet, run the following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="e7aa7-162">**FrontEnd** 서브넷의 속성만을 표시하는 예상된 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-162">Expected output showing only the properties of the **FrontEnd** subnet.</span></span> <span data-ttu-id="e7aa7-163">**NetworkSecurityGroup**에 대한 속성이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-163">Notice there isn't a property for **NetworkSecurityGroup**:</span></span>
   
            ...
            Subnets           : [
                                  {
                                    "Name": "FrontEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24",
                                    "IpConfigurations": [
                                      {
                                        "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1"
                                      },
                                      {
                                        "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1"
                                      }
                                    ],
                                    "ProvisioningState": "Succeeded"
                                  },
                                    ...
                                ]

### <a name="associate-an-nsg-to-a-subnet"></a><span data-ttu-id="e7aa7-164">서브넷에 NSG 연결</span><span class="sxs-lookup"><span data-stu-id="e7aa7-164">Associate an NSG to a subnet</span></span>
<span data-ttu-id="e7aa7-165">**NSG-FrontEnd** NSG를 **FronEnd** 서브넷에 다시 연결하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-165">To associate the **NSG-FrontEnd** NSG to the **FronEnd** subnet again, complete the following steps:</span></span>

1. <span data-ttu-id="e7aa7-166">다음 명령을 실행하여 기존 VNet 을 검색하고 변수에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-166">Run the following command to retrieve the existing VNet and store it in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. <span data-ttu-id="e7aa7-167">다음 명령을 실행하여 **FrontEnd** 서브넷을 검색하고 변수에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-167">Run the following command to retrieve the **FrontEnd** subnet and store it in a variable:</span></span>

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. <span data-ttu-id="e7aa7-168">다음 명령을 실행하여 기존 NSG를 검색하고 변수에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-168">Run the following command to retrieve the existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

4. <span data-ttu-id="e7aa7-169">**서브넷** 변수의 **NetworkSecurityGroup** 속성을 다음 명령을 실행하여 **$null** 변수의 값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-169">Set the **NetworkSecurityGroup** property of the **subnet** variable to **$null** by running the following command:</span></span>

    ```powershell
    $subnet.NetworkSecurityGroup = $nsg
    ```

5. <span data-ttu-id="e7aa7-170">서브넷에 대한 변경 사항을 저장하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-170">To save the changes made to the subnet, run the following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="e7aa7-171">**FrontEnd** 서브넷의 **NetworkSecurityGroup** 속성만을 표시하는 예상된 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-171">Expected output showing only the **NetworkSecurityGroup** property of the **FrontEnd** subnet:</span></span>
   
        ...
        "NetworkSecurityGroup": {
                                  "SecurityRules": [],
                                  "DefaultSecurityRules": [],
                                  "NetworkInterfaces": [],
                                  "Subnets": [],
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                }
        ...

## <a name="delete-an-nsg"></a><span data-ttu-id="e7aa7-172">NSG 삭제</span><span class="sxs-lookup"><span data-stu-id="e7aa7-172">Delete an NSG</span></span>
<span data-ttu-id="e7aa7-173">리소스에 연결되지 않은 경우 NSG를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-173">You can only delete an NSG if it's not associated to any resource.</span></span> <span data-ttu-id="e7aa7-174">NSG를 삭제하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-174">To delete an NSG, follow the steps below.</span></span>

1. <span data-ttu-id="e7aa7-175">NSG에 연결된 리소스를 확인하려면 [NSG 연결 보기](#View-NSGs-associations)에서처럼 `azure network nsg show`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-175">To check the resources associated to an NSG, run the `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="e7aa7-176">NSG가 NIC에 연결된 경우 각 NIC에 대한 [NIC에서 NSG 분리](#Dissociate-an-NSG-from-a-NIC)에서처럼 `azure network nic set`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-176">If the NSG is associated to any NICs, run the `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="e7aa7-177">NSG가 서브넷에 연결된 경우 각 서브넷에 대한 [서브넷에서 NSG 분리](#Dissociate-an-NSG-from-a-subnet)에서처럼 `azure network vnet subnet set`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-177">If the NSG is associated to any subnet, run the `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="e7aa7-178">NSG를 삭제하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-178">To delete the NSG, run the following command:</span></span>

    ```powershell
    Remove-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd -Force
    ```
   
   > [!NOTE]
   > <span data-ttu-id="e7aa7-179">`-Force` 매개 변수를 사용하면 삭제를 확인하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7aa7-179">The `-Force` parameter ensures you don't need to confirm the deletion.</span></span>
   > 

## <a name="next-steps"></a><span data-ttu-id="e7aa7-180">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e7aa7-180">Next steps</span></span>
* <span data-ttu-id="e7aa7-181">[로깅을 사용합니다](virtual-network-nsg-manage-log.md) .</span><span class="sxs-lookup"><span data-stu-id="e7aa7-181">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

