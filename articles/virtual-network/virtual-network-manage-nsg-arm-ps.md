---
title: "aaaManage 네트워크 보안 그룹-Azure PowerShell | Microsoft Docs"
description: "Toomanage PowerShell을 사용 하 여 보안 그룹을 네트워크 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 930fe5e0827896ad67b24d84e41a5d3f898ba838
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-powershell"></a><span data-ttu-id="29214-103">PowerShell을 사용하여 네트워크 보안 그룹 관리</span><span class="sxs-lookup"><span data-stu-id="29214-103">Manage network security groups using PowerShell</span></span>

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="29214-104">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29214-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="29214-105">이 문서에서는 Microsoft hello 클래식 배포 모델 대신 대부분의 새 배포에 권장 하는 hello 리소스 관리자 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="29214-105">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="29214-106">정보 검색</span><span class="sxs-lookup"><span data-stu-id="29214-106">Retrieve Information</span></span>
<span data-ttu-id="29214-107">기존 NSG를 보고 기존 NSG에 대한 규칙을 검색하며 NSG가 연결된 리소스에 대해 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29214-107">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="29214-108">기존 NSG 보기</span><span class="sxs-lookup"><span data-stu-id="29214-108">View existing NSGs</span></span>
<span data-ttu-id="29214-109">tooview 구독에서 모든 기존 Nsg 실행 hello `Get-AzureRmNetworkSecurityGroup` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="29214-109">tooview all existing NSGs in a subscription, run hello `Get-AzureRmNetworkSecurityGroup` cmdlet.</span></span>

<span data-ttu-id="29214-110">예상된 결과:</span><span class="sxs-lookup"><span data-stu-id="29214-110">Expected result:</span></span>

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


<span data-ttu-id="29214-111">Nsg hello 실행은 특정 리소스 그룹의 tooview hello 목록 `Get-AzureRmNetworkSecurityGroup` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="29214-111">tooview hello list of NSGs in a specific resource group, run hello `Get-AzureRmNetworkSecurityGroup` cmdlet.</span></span>

<span data-ttu-id="29214-112">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="29214-112">Expected output:</span></span>

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

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="29214-113">NSG에 대한 모든 규칙 나열</span><span class="sxs-lookup"><span data-stu-id="29214-113">List all rules for an NSG</span></span>
<span data-ttu-id="29214-114">명명 된 NSG의 tooview hello 규칙 **NSG 프런트 엔드**, hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="29214-114">tooview hello rules of an NSG named **NSG-FrontEnd**, enter hello following command:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd | Select SecurityRules -ExpandProperty SecurityRules
```

<span data-ttu-id="29214-115">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="29214-115">Expected output:</span></span>

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
> <span data-ttu-id="29214-116">사용할 수도 있습니다 `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` hello에서 toolist hello 기본 규칙 **NSG 프런트 엔드** NSG 합니다.</span><span class="sxs-lookup"><span data-stu-id="29214-116">You can also use `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` toolist hello default rules from hello **NSG-FrontEnd** NSG.</span></span>
> 

### <a name="view-nsgs-associations"></a><span data-ttu-id="29214-117">NSG 연결 보기</span><span class="sxs-lookup"><span data-stu-id="29214-117">View NSGs associations</span></span>
<span data-ttu-id="29214-118">tooview 어떤 리소스 hello **NSG 프런트 엔드** NSG와 연결, 실행 hello 다음 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="29214-118">tooview what resources hello **NSG-FrontEnd** NSG is associate with, run hello following command:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
```

<span data-ttu-id="29214-119">Hello에 대 한 확인 **NetworkInterfaces** 및 **서브넷** 아래와 같이 속성:</span><span class="sxs-lookup"><span data-stu-id="29214-119">Look for hello **NetworkInterfaces** and **Subnets** properties as shown below:</span></span>

    NetworkInterfaces    : []
    Subnets              : [
                             {
                               "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                               "IpConfigurations": []
                             }
                           ]

<span data-ttu-id="29214-120">Hello 이전 예에서 hello NSG는 되지 연결된 tooany Nic (네트워크 인터페이스); 명명 된 연결된 tooa 서브넷은 **프런트 엔드**합니다.</span><span class="sxs-lookup"><span data-stu-id="29214-120">In hello previous example, hello NSG is not associated tooany network interfaces (NICs); it is associated tooa subnet named **FrontEnd**.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="29214-121">규칙 관리</span><span class="sxs-lookup"><span data-stu-id="29214-121">Manage rules</span></span>
<span data-ttu-id="29214-122">기존 NSG 규칙 tooan 추가, 기존 규칙을 편집 하 고 규칙을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29214-122">You can add rules tooan existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="29214-123">규칙 추가</span><span class="sxs-lookup"><span data-stu-id="29214-123">Add a rule</span></span>
<span data-ttu-id="29214-124">허용 하는 규칙 tooadd **인바운드** 트래픽 tooport **443** 모든 컴퓨터 toohello에서 **NSG 프런트 엔드** NSG, 단계를 수행 하는 전체 hello:</span><span class="sxs-lookup"><span data-stu-id="29214-124">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, complete hello following steps:</span></span>

1. <span data-ttu-id="29214-125">다음 기존 NSG 명령 tooretrieve hello hello를 실행 하 고 변수에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="29214-125">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell   
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="29214-126">다음 명령은 tooadd hello 규칙 toohello NSG를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="29214-126">Run hello following command tooadd a rule toohello NSG:</span></span>

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

3. <span data-ttu-id="29214-127">toosave hello 변경 toohello NSG를 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="29214-127">toosave hello changes made toohello NSG, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```
    <span data-ttu-id="29214-128">보안 규칙만 hello를 보여 주는 예상된 출력:</span><span class="sxs-lookup"><span data-stu-id="29214-128">Expected output showing only hello security rules:</span></span>
   
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

### <a name="change-a-rule"></a><span data-ttu-id="29214-129">규칙 변경</span><span class="sxs-lookup"><span data-stu-id="29214-129">Change a rule</span></span>
<span data-ttu-id="29214-130">tooallow 위에서 만든 toochange hello 규칙 hello에서 트래픽 인바운드 **인터넷** 만 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="29214-130">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, follow hello steps below.</span></span>

1. <span data-ttu-id="29214-131">다음 기존 NSG 명령 tooretrieve hello hello를 실행 하 고 변수에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="29214-131">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell 
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="29214-132">Hello 다음 hello 새 규칙 설정으로 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="29214-132">Run hello following command with hello new rule settings:</span></span>

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

3. <span data-ttu-id="29214-133">toosave hello 변경 toohello NSG를 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="29214-133">toosave hello changes made toohello NSG, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="29214-134">보안 규칙만 hello를 보여 주는 예상된 출력:</span><span class="sxs-lookup"><span data-stu-id="29214-134">Expected output showing only hello security rules:</span></span>
   
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

### <a name="delete-a-rule"></a><span data-ttu-id="29214-135">규칙 삭제</span><span class="sxs-lookup"><span data-stu-id="29214-135">Delete a rule</span></span>
1. <span data-ttu-id="29214-136">다음 기존 NSG 명령 tooretrieve hello hello를 실행 하 고 변수에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="29214-136">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="29214-137">Hello 명령 tooremove hello 규칙 hello NSG에서에서 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="29214-137">Run hello following command tooremove hello rule from hello NSG:</span></span>

    ```powershell
    Remove-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg -Name https-rule
    ```

3. <span data-ttu-id="29214-138">Hello 다음 명령을 실행 하 여 hello 변경 내용을 toohello NSG를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="29214-138">Save hello changes made toohello NSG, by running hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="29214-139">보안 규칙 통지 hello만 hello를 보여 주는 예상된 출력 **https 규칙** 더 이상 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="29214-139">Expected output showing only hello security rules, notice hello **https-rule** is no longer listed:</span></span>
   
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

## <a name="manage-associations"></a><span data-ttu-id="29214-140">연결 관리</span><span class="sxs-lookup"><span data-stu-id="29214-140">Manage associations</span></span>
<span data-ttu-id="29214-141">NSG toosubnets 및 Nic를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29214-141">You can associate an NSG toosubnets and NICs.</span></span> <span data-ttu-id="29214-142">또한 연결된 모든 리소스에서 NSG를 분리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29214-142">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="29214-143">NSG tooa NIC에 연결</span><span class="sxs-lookup"><span data-stu-id="29214-143">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="29214-144">tooassociate hello **NSG 프런트 엔드** NSG toohello **TestNICWeb1** NIC를 다음 단계 완료 hello:</span><span class="sxs-lookup"><span data-stu-id="29214-144">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="29214-145">다음 기존 NSG 명령 tooretrieve hello hello를 실행 하 고 변수에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="29214-145">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="29214-146">Hello 명령 tooretrieve hello 기존 NIC를 다음을 실행 하 고 변수에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="29214-146">Run hello following command tooretrieve hello existing NIC and store it in a variable:</span></span>

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

3. <span data-ttu-id="29214-147">집합 hello **NetworkSecurityGroup** hello 속성 **NIC** hello 변수 toohello 값 **NSG** hello 다음 명령을 입력 하 여 변수:</span><span class="sxs-lookup"><span data-stu-id="29214-147">Set hello **NetworkSecurityGroup** property of hello **NIC** variable toohello value of hello **NSG** variable, by entering hello following command:</span></span>

    ```powershell
    $nic.NetworkSecurityGroup = $nsg
    ```

4. <span data-ttu-id="29214-148">toosave hello 변경 toohello NIC를 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="29214-148">toosave hello changes made toohello NIC, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    <span data-ttu-id="29214-149">예상된 출력이 보여 주는 hello **NetworkSecurityGroup** 속성:</span><span class="sxs-lookup"><span data-stu-id="29214-149">Expected output showing only hello **NetworkSecurityGroup** property:</span></span>
   
        NetworkSecurityGroup : {
                                 "SecurityRules": [],
                                 "DefaultSecurityRules": [],
                                 "NetworkInterfaces": [],
                                 "Subnets": [],
                                 "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                               }

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="29214-150">NIC에서 NSG 분리</span><span class="sxs-lookup"><span data-stu-id="29214-150">Dissociate an NSG from a NIC</span></span>
<span data-ttu-id="29214-151">toodissociate hello **NSG 프런트 엔드** hello에서 NSG **TestNICWeb1** NIC를 다음 단계 완료 hello:</span><span class="sxs-lookup"><span data-stu-id="29214-151">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="29214-152">Hello 명령 tooretrieve hello 기존 NIC를 다음을 실행 하 고 변수에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="29214-152">Run hello following command tooretrieve hello existing NIC and store it in a variable:</span></span>

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

2. <span data-ttu-id="29214-153">집합 hello **NetworkSecurityGroup** hello 속성 **NIC** 변수 너무**$null** hello 다음 명령을 실행 하 여:</span><span class="sxs-lookup"><span data-stu-id="29214-153">Set hello **NetworkSecurityGroup** property of hello **NIC** variable too**$null** by running hello following command:</span></span>

    ```powershell
    $nic.NetworkSecurityGroup = $null
    ```

3. <span data-ttu-id="29214-154">toosave hello 변경 toohello NIC를 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="29214-154">toosave hello changes made toohello NIC, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    <span data-ttu-id="29214-155">예상된 출력이 보여 주는 hello **NetworkSecurityGroup** 속성:</span><span class="sxs-lookup"><span data-stu-id="29214-155">Expected output showing only hello **NetworkSecurityGroup** property:</span></span>
   
        NetworkSecurityGroup : null

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="29214-156">서브넷에서 NSG 분리</span><span class="sxs-lookup"><span data-stu-id="29214-156">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="29214-157">toodissociate hello **NSG 프런트 엔드** hello에서 NSG **프런트 엔드** 서브넷, 단계를 수행 하는 전체 hello:</span><span class="sxs-lookup"><span data-stu-id="29214-157">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, complete hello following steps:</span></span>

1. <span data-ttu-id="29214-158">Hello 명령 tooretrieve hello 기존 VNet을 다음을 실행 하 고 변수에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="29214-158">Run hello following command tooretrieve hello existing VNet and store it in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. <span data-ttu-id="29214-159">실행 hello 명령 tooretrieve hello 다음 **프런트 엔드** 서브넷 변수에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="29214-159">Run hello following command tooretrieve hello **FrontEnd** subnet and store it in a variable:</span></span>

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. <span data-ttu-id="29214-160">집합 hello **NetworkSecurityGroup** hello 속성 **서브넷** 변수 너무**$null** hello 다음 명령을 입력 하 여:</span><span class="sxs-lookup"><span data-stu-id="29214-160">Set hello **NetworkSecurityGroup** property of hello **subnet** variable too**$null** by entering hello following command:</span></span>

    ```powershell
    $subnet.NetworkSecurityGroup = $null
    ```

4. <span data-ttu-id="29214-161">toosave hello 변경 서브넷 toohello hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="29214-161">toosave hello changes made toohello subnet, run hello following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="29214-162">Hello의 hello 속성만 보여 주는 예상된 출력 **프런트 엔드** 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="29214-162">Expected output showing only hello properties of hello **FrontEnd** subnet.</span></span> <span data-ttu-id="29214-163">**NetworkSecurityGroup**에 대한 속성이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="29214-163">Notice there isn't a property for **NetworkSecurityGroup**:</span></span>
   
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

### <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="29214-164">NSG tooa 서브넷 연결</span><span class="sxs-lookup"><span data-stu-id="29214-164">Associate an NSG tooa subnet</span></span>
<span data-ttu-id="29214-165">tooassociate hello **NSG 프런트 엔드** NSG toohello **FronEnd** 다시 서브넷, 단계를 수행 하는 전체 hello:</span><span class="sxs-lookup"><span data-stu-id="29214-165">tooassociate hello **NSG-FrontEnd** NSG toohello **FronEnd** subnet again, complete hello following steps:</span></span>

1. <span data-ttu-id="29214-166">Hello 명령 tooretrieve hello 기존 VNet을 다음을 실행 하 고 변수에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="29214-166">Run hello following command tooretrieve hello existing VNet and store it in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. <span data-ttu-id="29214-167">실행 hello 명령 tooretrieve hello 다음 **프런트 엔드** 서브넷 변수에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="29214-167">Run hello following command tooretrieve hello **FrontEnd** subnet and store it in a variable:</span></span>

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. <span data-ttu-id="29214-168">다음 기존 NSG 명령 tooretrieve hello hello를 실행 하 고 변수에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="29214-168">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

4. <span data-ttu-id="29214-169">집합 hello **NetworkSecurityGroup** hello 속성 **서브넷** 변수 너무**$null** hello 다음 명령을 실행 하 여:</span><span class="sxs-lookup"><span data-stu-id="29214-169">Set hello **NetworkSecurityGroup** property of hello **subnet** variable too**$null** by running hello following command:</span></span>

    ```powershell
    $subnet.NetworkSecurityGroup = $nsg
    ```

5. <span data-ttu-id="29214-170">toosave hello 변경 서브넷 toohello hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="29214-170">toosave hello changes made toohello subnet, run hello following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="29214-171">예상된 출력이 보여 주는 hello **NetworkSecurityGroup** hello 속성 **프런트 엔드** 서브넷:</span><span class="sxs-lookup"><span data-stu-id="29214-171">Expected output showing only hello **NetworkSecurityGroup** property of hello **FrontEnd** subnet:</span></span>
   
        ...
        "NetworkSecurityGroup": {
                                  "SecurityRules": [],
                                  "DefaultSecurityRules": [],
                                  "NetworkInterfaces": [],
                                  "Subnets": [],
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                }
        ...

## <a name="delete-an-nsg"></a><span data-ttu-id="29214-172">NSG 삭제</span><span class="sxs-lookup"><span data-stu-id="29214-172">Delete an NSG</span></span>
<span data-ttu-id="29214-173">NSG tooany 리소스를 연결 되지 않은 경우에 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29214-173">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="29214-174">NSG를 toodelete는 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="29214-174">toodelete an NSG, follow hello steps below.</span></span>

1. <span data-ttu-id="29214-175">toocheck hello 리소스 관련 tooan NSG를 hello 실행 `azure network nsg show` 에서처럼 [보기 Nsg 연결](#View-NSGs-associations)합니다.</span><span class="sxs-lookup"><span data-stu-id="29214-175">toocheck hello resources associated tooan NSG, run hello `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="29214-176">Hello NSG 연결된 tooany Nic 이면 hello 실행 `azure network nic set` 에서처럼 [NIC에서 NSG를 분리](#Dissociate-an-NSG-from-a-NIC) 각 NIC.에 대 한</span><span class="sxs-lookup"><span data-stu-id="29214-176">If hello NSG is associated tooany NICs, run hello `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="29214-177">Hello NSG 연결된 tooany 서브넷 이면 hello 실행 `azure network vnet subnet set` 에서처럼 [서브넷에서 NSG를 분리](#Dissociate-an-NSG-from-a-subnet) 각 서브넷에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="29214-177">If hello NSG is associated tooany subnet, run hello `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="29214-178">toodelete hello NSG hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="29214-178">toodelete hello NSG, run hello following command:</span></span>

    ```powershell
    Remove-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd -Force
    ```
   
   > [!NOTE]
   > <span data-ttu-id="29214-179">hello `-Force` 매개 변수를 사용 하면 tooconfirm hello 삭제 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="29214-179">hello `-Force` parameter ensures you don't need tooconfirm hello deletion.</span></span>
   > 

## <a name="next-steps"></a><span data-ttu-id="29214-180">다음 단계</span><span class="sxs-lookup"><span data-stu-id="29214-180">Next steps</span></span>
* <span data-ttu-id="29214-181">[로깅을 사용합니다](virtual-network-nsg-manage-log.md) .</span><span class="sxs-lookup"><span data-stu-id="29214-181">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

