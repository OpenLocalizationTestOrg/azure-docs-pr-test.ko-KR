---
title: "aaaManage 네트워크 보안 그룹-Azure CLI 1.0 | Microsoft Docs"
description: "Toomanage 네트워크 보안 그룹을 사용 하 여 Azure CLI (명령줄 인터페이스) 1.0 hello 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 9a429f947abbcb5fa6adb40c84504f68efd5e20e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-hello-azure-cli-10"></a><span data-ttu-id="2e4dd-103">Hello Azure CLI 1.0을 사용 하 여 네트워크 보안 그룹 관리</span><span class="sxs-lookup"><span data-stu-id="2e4dd-103">Manage network security groups using hello Azure CLI 1.0</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="2e4dd-104">CLI 버전 toocomplete hello 작업</span><span class="sxs-lookup"><span data-stu-id="2e4dd-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="2e4dd-105">Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e4dd-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="2e4dd-106">[Azure CLI 1.0](#View-existing-NSGs) – hello 클래식 및 리소스 관리 배포 모델에 대 한 우리의 CLI</span><span class="sxs-lookup"><span data-stu-id="2e4dd-106">[Azure CLI 1.0](#View-existing-NSGs) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="2e4dd-107">[Azure CLI 2.0](virtual-network-manage-nsg-arm-cli.md) -우리의 차세대 CLI hello 리소스 관리 배포 모델 (이 문서)</span><span class="sxs-lookup"><span data-stu-id="2e4dd-107">[Azure CLI 2.0](virtual-network-manage-nsg-arm-cli.md) - our next generation CLI for hello resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="2e4dd-108">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e4dd-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="2e4dd-109">이 문서에서는 Microsoft hello 클래식 배포 모델 대신 대부분의 새 배포에 권장 하는 hello 리소스 관리자 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e4dd-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="2e4dd-110">정보 검색</span><span class="sxs-lookup"><span data-stu-id="2e4dd-110">Retrieve Information</span></span>
<span data-ttu-id="2e4dd-111">기존 NSG를 보고 기존 NSG에 대한 규칙을 검색하며 NSG가 연결된 리소스에 대해 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e4dd-111">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="2e4dd-112">기존 NSG 보기</span><span class="sxs-lookup"><span data-stu-id="2e4dd-112">View existing NSGs</span></span>
<span data-ttu-id="2e4dd-113">Nsg hello 실행은 특정 리소스 그룹의 tooview hello 목록 `azure network nsg list` 아래와 같이 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="2e4dd-113">tooview hello list of NSGs in a specific resource group, run hello `azure network nsg list` command as shown below.</span></span>

```azurecli
azure network nsg list --resource-group RG-NSG
```

<span data-ttu-id="2e4dd-114">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="2e4dd-114">Expected output:</span></span>

    info:    Executing command network nsg list
    + Getting hello network security groups
    data:    Name          Location
    data:    ------------  --------
    data:    NSG-BackEnd   westus
    data:    NSG-FrontEnd  westus
    info:    network nsg list command OK

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="2e4dd-115">NSG에 대한 모든 규칙 나열</span><span class="sxs-lookup"><span data-stu-id="2e4dd-115">List all rules for an NSG</span></span>
<span data-ttu-id="2e4dd-116">명명 된 NSG의 tooview hello 규칙 **NSG 프런트 엔드**실행 hello `azure network nsg show` 아래와 같이 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="2e4dd-116">tooview hello rules of an NSG named **NSG-FrontEnd**, run hello `azure network nsg show` command as shown below.</span></span> 

```azurecli
azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd
```

<span data-ttu-id="2e4dd-117">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="2e4dd-117">Expected output:</span></span>

    info:    Executing command network nsg show
    + Looking up hello network security group "NSG-FrontEnd"
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
> <span data-ttu-id="2e4dd-118">사용할 수도 있습니다 `azure network nsg rule list --resource-group RG-NSG --nsg-name NSG-FrontEnd` hello에서 toolist hello 규칙 **NSG 프런트 엔드** NSG 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e4dd-118">You can also use `azure network nsg rule list --resource-group RG-NSG --nsg-name NSG-FrontEnd` toolist hello rules from hello **NSG-FrontEnd** NSG.</span></span>
>

### <a name="view-nsg-associations"></a><span data-ttu-id="2e4dd-119">NSG 연결 보기</span><span class="sxs-lookup"><span data-stu-id="2e4dd-119">View NSG associations</span></span>

<span data-ttu-id="2e4dd-120">tooview 어떤 리소스 hello **NSG 프런트 엔드** NSG는 연결 된를 실행 하는 hello `azure network nsg show` 아래와 같이 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="2e4dd-120">tooview what resources hello **NSG-FrontEnd** NSG is associate with, run hello `azure network nsg show` command as shown below.</span></span> <span data-ttu-id="2e4dd-121">차이점은 hello hello 사용에만 해당 hello 확인 **-json** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="2e4dd-121">Notice that hello only difference is hello use of hello **--json** parameter.</span></span>

```azurecli
azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json
```

<span data-ttu-id="2e4dd-122">Hello에 대 한 확인 **networkInterfaces** 및 **서브넷** 아래와 같이 속성:</span><span class="sxs-lookup"><span data-stu-id="2e4dd-122">Look for hello **networkInterfaces** and **subnets** properties as shown below:</span></span>

    "networkInterfaces": [],
    ...
    "subnets": [
        {
            "id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
        }
    ],
    ...

<span data-ttu-id="2e4dd-123">NSG가 hello tooany Nic (네트워크 인터페이스), 연결 된 위의 hello 예제 이며 라는 관련된 tooa 서브넷 **프런트 엔드**합니다.</span><span class="sxs-lookup"><span data-stu-id="2e4dd-123">In hello example above, hello NSG is not associated tooany network interfaces (NICs), and it is associated tooa subnet named **FrontEnd**.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="2e4dd-124">규칙 관리</span><span class="sxs-lookup"><span data-stu-id="2e4dd-124">Manage rules</span></span>
<span data-ttu-id="2e4dd-125">기존 NSG 규칙 tooan 추가, 기존 규칙을 편집 하 고 규칙을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e4dd-125">You can add rules tooan existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="2e4dd-126">규칙 추가</span><span class="sxs-lookup"><span data-stu-id="2e4dd-126">Add a rule</span></span>
<span data-ttu-id="2e4dd-127">tooadd 허용 하는 규칙 **인바운드** 트래픽 tooport **443** 모든 컴퓨터 toohello에서 **NSG 프런트 엔드** NSG를 hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e4dd-127">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, enter hello following command:</span></span>

```azurecli
azure network nsg rule create --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --description "Allow access tooport 443 for HTTPS" \
    --protocol Tcp \
    --source-address-prefix * \
    --source-port-range * \
    --destination-address-prefix * \
    --destination-port-range 443 \
    --access Allow \
    --priority 102 \
    --direction Inbound
```

<span data-ttu-id="2e4dd-128">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="2e4dd-128">Expected output:</span></span>

    info:    Executing command network nsg rule create
    + Looking up hello network security rule "allow-https"
    + Creating a network security rule "allow-https"
    + Looking up hello network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https
    data:    Name                            : allow-https
    data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
    data:    Provisioning state              : Succeeded
    data:    Description                     : Allow access tooport 443 for HTTPS
    data:    Source IP                       : *
    data:    Source Port                     : *
    data:    Destination IP                  : *
    data:    Destination Port                : 443
    data:    Protocol                        : Tcp
    data:    Direction                       : Inbound
    data:    Access                          : Allow
    data:    Priority                        : 102
    info:    network nsg rule create command OK

### <a name="change-a-rule"></a><span data-ttu-id="2e4dd-129">규칙 변경</span><span class="sxs-lookup"><span data-stu-id="2e4dd-129">Change a rule</span></span>
<span data-ttu-id="2e4dd-130">tooallow 위에서 만든 toochange hello 규칙 hello에서 트래픽 인바운드 **인터넷** 만, 런타임 hello 다음 명령을:</span><span class="sxs-lookup"><span data-stu-id="2e4dd-130">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, run hello following command:</span></span>

```azurecli
azure network nsg rule set --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --source-address-prefix Internet
```

<span data-ttu-id="2e4dd-131">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="2e4dd-131">Expected output:</span></span>

    info:    Executing command network nsg rule set
    + Looking up hello network security group "NSG-FrontEnd"
    + Setting a network security rule "allow-https"
    + Looking up hello network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https
    data:    Name                            : allow-https
    data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
    data:    Provisioning state              : Succeeded
    data:    Description                     : Allow access tooport 443 for HTTPS
    data:    Source IP                       : Internet
    data:    Source Port                     : *
    data:    Destination IP                  : *
    data:    Destination Port                : 443
    data:    Protocol                        : Tcp
    data:    Direction                       : Inbound
    data:    Access                          : Allow
    data:    Priority                        : 102
    info:    network nsg rule set command OK

### <a name="delete-a-rule"></a><span data-ttu-id="2e4dd-132">규칙 삭제</span><span class="sxs-lookup"><span data-stu-id="2e4dd-132">Delete a rule</span></span>
<span data-ttu-id="2e4dd-133">위에서 만든 toodelete hello 규칙은 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e4dd-133">toodelete hello rule created above, run hello following command:</span></span>

```azurecli
azure network nsg rule delete --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --quiet
```

> [!NOTE]
> <span data-ttu-id="2e4dd-134">hello `--quiet` 매개 변수를 사용 하면 tooconfirm hello 삭제 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2e4dd-134">hello `--quiet` parameter ensures you don't need tooconfirm hello deletion.</span></span>
>

<span data-ttu-id="2e4dd-135">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="2e4dd-135">Expected output:</span></span>

    info:    Executing command network nsg rule delete
    + Looking up hello network security group "NSG-FrontEnd"
    + Deleting network security rule "allow-https"
    info:    network nsg rule delete command OK

## <a name="manage-associations"></a><span data-ttu-id="2e4dd-136">연결 관리</span><span class="sxs-lookup"><span data-stu-id="2e4dd-136">Manage associations</span></span>
<span data-ttu-id="2e4dd-137">NSG toosubnets 및 Nic를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e4dd-137">You can associate an NSG toosubnets and NICs.</span></span> <span data-ttu-id="2e4dd-138">또한 연결된 모든 리소스에서 NSG를 분리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e4dd-138">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="2e4dd-139">NSG tooa NIC에 연결</span><span class="sxs-lookup"><span data-stu-id="2e4dd-139">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="2e4dd-140">tooassociate hello **NSG 프런트 엔드** NSG toohello **TestNICWeb1** NIC를 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e4dd-140">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, run hello following command:</span></span>

```azurecli
azure network nic set --resource-group RG-NSG \
    --name TestNICWeb1 \
    --network-security-group-name NSG-FrontEnd
```

<span data-ttu-id="2e4dd-141">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="2e4dd-141">Expected output:</span></span>

    info:    Executing command network nic set
    + Looking up hello network interface "TestNICWeb1"
    + Looking up hello network security group "NSG-FrontEnd"
    + Updating network interface "TestNICWeb1"
    + Looking up hello network interface "TestNICWeb1"
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

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="2e4dd-142">NIC에서 NSG 분리</span><span class="sxs-lookup"><span data-stu-id="2e4dd-142">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="2e4dd-143">toodissociate hello **NSG 프런트 엔드** hello에서 NSG **TestNICWeb1** NIC를 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e4dd-143">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, run hello following command:</span></span>

```azurecli
azure network nic set --resource-group RG-NSG --name TestNICWeb1 --network-security-group-id ""
```

> [!NOTE]
> <span data-ttu-id="2e4dd-144">공지 hello "" hello에 대 한 (비어 있음) 값 `network-security-group-id` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="2e4dd-144">Notice hello "" (empty) value for hello `network-security-group-id` parameter.</span></span> <span data-ttu-id="2e4dd-145">연결 tooan NSG를 제거 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="2e4dd-145">That is how you remove an association tooan NSG.</span></span> <span data-ttu-id="2e4dd-146">작업할 수 없는 hello로 동일 hello `network-security-group-name` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="2e4dd-146">You can't do hello same with hello `network-security-group-name` parameter.</span></span>
> 

<span data-ttu-id="2e4dd-147">예상된 결과:</span><span class="sxs-lookup"><span data-stu-id="2e4dd-147">Expected result:</span></span>

    info:    Executing command network nic set
    + Looking up hello network interface "TestNICWeb1"
    + Updating network interface "TestNICWeb1"
    + Looking up hello network interface "TestNICWeb1"
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

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="2e4dd-148">서브넷에서 NSG 분리</span><span class="sxs-lookup"><span data-stu-id="2e4dd-148">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="2e4dd-149">toodissociate hello **NSG 프런트 엔드** hello에서 NSG **프런트 엔드** 서브넷 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e4dd-149">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, run hello following command:</span></span>

```azurecli
azure network vnet subnet set --resource-group RG-NSG \
    --vnet-name TestVNet \
    --name FrontEnd \
    --network-security-group-id ""
```

<span data-ttu-id="2e4dd-150">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="2e4dd-150">Expected output:</span></span>

    info:    Executing command network vnet subnet set
    + Looking up hello subnet "FrontEnd"
    + Setting subnet "FrontEnd"
    + Looking up hello subnet "FrontEnd"
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

### <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="2e4dd-151">NSG tooa 서브넷 연결</span><span class="sxs-lookup"><span data-stu-id="2e4dd-151">Associate an NSG tooa subnet</span></span>
<span data-ttu-id="2e4dd-152">tooassociate hello **NSG 프런트 엔드** NSG toohello **FronEnd** 서브넷에 hello 다음 명령을 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e4dd-152">tooassociate hello **NSG-FrontEnd** NSG toohello **FronEnd** subnet again, run hello following command:</span></span>

```azurecli
azure network vnet subnet set --resource-group RG-NSG \
    --vnet-name TestVNet \
    --name FrontEnd \
    --network-security-group-name NSG-FronEnd
```

> [!NOTE]
> <span data-ttu-id="2e4dd-153">hello 위의 명령에만 작동 하기 때문에 hello **NSG 프런트 엔드** hello에 NSG가 hello 가상 네트워크와 동일한 리소스 그룹 **TestVNet**합니다.</span><span class="sxs-lookup"><span data-stu-id="2e4dd-153">hello command above only works because hello **NSG-FrontEnd** NSG is in hello same resource group as hello virtual network **TestVNet**.</span></span> <span data-ttu-id="2e4dd-154">Toouse hello hello NSG 다른 리소스 그룹에 포함 된 경우에 필요 `--network-security-group-id` 매개 변수 대신 NSG hello에 대 한 hello 전체 id를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e4dd-154">If hello NSG is in a different resource group, you need toouse hello `--network-security-group-id` parameter instead, and provide hello full id for hello NSG.</span></span> <span data-ttu-id="2e4dd-155">실행 하 여 hello id를 검색할 수 있습니다 `azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json` hello를 찾아 **id** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="2e4dd-155">You can retrieve hello id by running `azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json` and looking for hello **id** property.</span></span> 
> 

<span data-ttu-id="2e4dd-156">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="2e4dd-156">Expected output:</span></span>

        info:    Executing command network vnet subnet set
        + Looking up hello subnet "FrontEnd"
        + Looking up hello network security group "NSG-FrontEnd"
        + Setting subnet "FrontEnd"
        + Looking up hello subnet "FrontEnd"
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

## <a name="delete-an-nsg"></a><span data-ttu-id="2e4dd-157">NSG 삭제</span><span class="sxs-lookup"><span data-stu-id="2e4dd-157">Delete an NSG</span></span>
<span data-ttu-id="2e4dd-158">NSG tooany 리소스를 연결 되지 않은 경우에 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e4dd-158">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="2e4dd-159">NSG를 toodelete는 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e4dd-159">toodelete an NSG, follow hello steps below.</span></span>

1. <span data-ttu-id="2e4dd-160">toocheck hello 리소스 관련 tooan NSG를 hello 실행 `azure network nsg show` 에서처럼 [보기 Nsg 연결](#View-NSGs-associations)합니다.</span><span class="sxs-lookup"><span data-stu-id="2e4dd-160">toocheck hello resources associated tooan NSG, run hello `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="2e4dd-161">Hello NSG 연결된 tooany Nic 이면 hello 실행 `azure network nic set` 에서처럼 [NIC에서 NSG를 분리](#Dissociate-an-NSG-from-a-NIC) 각 NIC.에 대 한</span><span class="sxs-lookup"><span data-stu-id="2e4dd-161">If hello NSG is associated tooany NICs, run hello `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="2e4dd-162">Hello NSG 연결된 tooany 서브넷 이면 hello 실행 `azure network vnet subnet set` 에서처럼 [서브넷에서 NSG를 분리](#Dissociate-an-NSG-from-a-subnet) 각 서브넷에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e4dd-162">If hello NSG is associated tooany subnet, run hello `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="2e4dd-163">toodelete hello NSG hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e4dd-163">toodelete hello NSG, run hello following command:</span></span>

    ```azurecli
    azure network nsg delete --resource-group RG-NSG --name NSG-FrontEnd --quiet
    ```

    <span data-ttu-id="2e4dd-164">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="2e4dd-164">Expected output:</span></span>

        info:    Executing command network nsg delete
        + Looking up hello network security group "NSG-FrontEnd"
        + Deleting network security group "NSG-FrontEnd"
        info:    network nsg delete command OK

## <a name="next-steps"></a><span data-ttu-id="2e4dd-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2e4dd-165">Next steps</span></span>
* <span data-ttu-id="2e4dd-166">[로깅을 사용합니다](virtual-network-nsg-manage-log.md) .</span><span class="sxs-lookup"><span data-stu-id="2e4dd-166">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

