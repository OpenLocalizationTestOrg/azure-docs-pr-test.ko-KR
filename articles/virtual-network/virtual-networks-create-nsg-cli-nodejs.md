---
title: "aaaCreate 네트워크 보안 그룹-Azure CLI 1.0 | Microsoft Docs"
description: "자세한 방법을 toocreate hello Azure CLI 1.0을 사용 하 여 네트워크 보안 그룹을 배포 합니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/17/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: eeb7feedab959d92659e03c5c46d93fdfc08faea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-hello-azure-cli-10"></a><span data-ttu-id="77078-103">네트워크를 Azure CLI 1.0 hello를 사용 하 여 보안 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="77078-103">Create network security groups using hello Azure CLI 1.0</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="77078-104">CLI 버전 toocomplete hello 작업</span><span class="sxs-lookup"><span data-stu-id="77078-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="77078-105">Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77078-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="77078-106">[Azure CLI 1.0](#how-to-create-the-nsg-for-the-front-end-subnet) – 우리의 CLI 모델에 대 한 hello 클래식 및 리소스 관리 배포 (이 문서)</span><span class="sxs-lookup"><span data-stu-id="77078-106">[Azure CLI 1.0](#how-to-create-the-nsg-for-the-front-end-subnet) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="77078-107">[Azure CLI 2.0](virtual-networks-create-nsg-arm-cli.md) -hello 리소스 관리 배포 모델에 대 한 우리의 차세대 CLI</span><span class="sxs-lookup"><span data-stu-id="77078-107">[Azure CLI 2.0](virtual-networks-create-nsg-arm-cli.md) - our next-generation CLI for hello resource management deployment model</span></span> 

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="77078-108">이 문서에서는 hello 리소스 관리자 배포 모델에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="77078-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="77078-109">수도 있습니다 [hello 클래식 배포 모델에서 Nsg를 만들](virtual-networks-create-nsg-classic-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="77078-109">You can also [create NSGs in hello classic deployment model](virtual-networks-create-nsg-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="77078-110">hello 샘플 Azure CLI 명령 아래에 이미 위의 hello 시나리오를 기반으로 만들어진 단순 환경이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="77078-110">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> 

## <a name="how-toocreate-hello-nsg-for-hello-front-end-subnet"></a><span data-ttu-id="77078-111">Toocreate NSG hello 프런트 엔드 서브넷에 대 한 hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="77078-111">How toocreate hello NSG for hello front end subnet</span></span>
<span data-ttu-id="77078-112">명명 된 NSG 라는 toocreate *NSG 프런트 엔드* 아래 hello 단계에 따라 위의 hello 시나리오에 따라, 합니다.</span><span class="sxs-lookup"><span data-stu-id="77078-112">toocreate an NSG named named *NSG-FrontEnd* based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="77078-113">Azure CLI 처음 사용 하는 경우 참조 [설치 및 구성 hello Azure CLI](../cli-install-nodejs.md) Azure 계정 및 구독을 선택 하면 toohello 포인트 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="77078-113">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="77078-114">Hello 실행 **azure 구성 모드** 명령 tooswitch tooResource 관리자 모드에서는 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="77078-114">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>
   
        azure config mode arm
   
    <span data-ttu-id="77078-115">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="77078-115">Expected output:</span></span>
   
        info:    New mode is arm
3. <span data-ttu-id="77078-116">Hello 실행 **azure 네트워크 nsg 만들기** 명령 toocreate NSG 합니다.</span><span class="sxs-lookup"><span data-stu-id="77078-116">Run hello **azure network nsg create** command toocreate an NSG.</span></span>
   
        azure network nsg create -g TestRG -l westus -n NSG-FrontEnd
   
    <span data-ttu-id="77078-117">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="77078-117">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
        data:    Name                            : NSG-FrontEnd
        data:    Type                            : Microsoft.Network/networkSecurityGroups
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Security group rules:
        data:    Name                           Source IP          Source Port  Destination IP  Destination Port  Protocol  Direction  Access  Priority
        data:    -----------------------------  -----------------  -----------  --------------  ----------------  --------  ---------  ------  --------
        data:    AllowVnetInBound               VirtualNetwork     *            VirtualNetwork  *                 *         Inbound    Allow   65000   
        data:    AllowAzureLoadBalancerInBound  AzureLoadBalancer  *            *               *                 *         Inbound    Allow   65001   
        data:    DenyAllInBound                 *                  *            *               *                 *         Inbound    Deny    65500   
        data:    AllowVnetOutBound              VirtualNetwork     *            VirtualNetwork  *                 *         Outbound   Allow   65000   
        data:    AllowInternetOutBound          *                  *            Internet        *                 *         Outbound   Allow   65001   
        data:    DenyAllOutBound                *                  *            *               *                 *         Outbound   Deny    65500   
        info:    network nsg create command OK
   
    <span data-ttu-id="77078-118">매개 변수</span><span class="sxs-lookup"><span data-stu-id="77078-118">Parameters:</span></span>
   
   * <span data-ttu-id="77078-119">**-g (or --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="77078-119">**-g (or --resource-group)**.</span></span> <span data-ttu-id="77078-120">NSG hello 만들어지는 hello 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="77078-120">Name of hello resource group where hello NSG will be created.</span></span> <span data-ttu-id="77078-121">이 시나리오에서는 *TestRG*입니다.</span><span class="sxs-lookup"><span data-stu-id="77078-121">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="77078-122">**-l(또는 --location)**.</span><span class="sxs-lookup"><span data-stu-id="77078-122">**-l (or --location)**.</span></span> <span data-ttu-id="77078-123">Azure 지역 hello 새 NSG를 만들 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="77078-123">Azure region where hello new NSG will be created.</span></span> <span data-ttu-id="77078-124">이 시나리오에서는 *westus*입니다.</span><span class="sxs-lookup"><span data-stu-id="77078-124">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="77078-125">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="77078-125">**-n (or --name)**.</span></span> <span data-ttu-id="77078-126">Hello에 대 한 이름을 새 NSG 합니다.</span><span class="sxs-lookup"><span data-stu-id="77078-126">Name for hello new NSG.</span></span> <span data-ttu-id="77078-127">이 시나리오에서는 *NSG-FrontEnd*입니다.</span><span class="sxs-lookup"><span data-stu-id="77078-127">For our scenario, *NSG-FrontEnd*.</span></span>
4. <span data-ttu-id="77078-128">Hello 실행 **azure 네트워크 nsg 규칙 만들기** 명령 toocreate hello 인터넷에서에서 액세스 tooport 3389 (RDP)를 허용 하는 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="77078-128">Run hello **azure network nsg rule create** command toocreate a rule that allows access tooport 3389 (RDP) from hello Internet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    <span data-ttu-id="77078-129">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="77078-129">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        warn:    Using default direction: Inbound
        info:    Looking up hello network security rule "rdp-rule"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp
        -rule
        data:    Name                            : rdp-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : Internet
        data:    Source Port                     : *
        data:    Destination IP                  : *
        data:    Destination Port                : 3389
        data:    Protocol                        : Tcp
        data:    Direction                       : Inbound
        data:    Access                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
   
    <span data-ttu-id="77078-130">매개 변수</span><span class="sxs-lookup"><span data-stu-id="77078-130">Parameters:</span></span>
   
   * <span data-ttu-id="77078-131">**-a(또는 --nsg-name)**.</span><span class="sxs-lookup"><span data-stu-id="77078-131">**-a (or --nsg-name)**.</span></span> <span data-ttu-id="77078-132">Hello NSG 규칙 만들 수 있는 hello의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="77078-132">Name of hello NSG in which hello rule will be created.</span></span> <span data-ttu-id="77078-133">이 시나리오에서는 *NSG-FrontEnd*입니다.</span><span class="sxs-lookup"><span data-stu-id="77078-133">For our scenario, *NSG-FrontEnd*.</span></span>
   * <span data-ttu-id="77078-134">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="77078-134">**-n (or --name)**.</span></span> <span data-ttu-id="77078-135">Hello 새 규칙의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="77078-135">Name for hello new rule.</span></span> <span data-ttu-id="77078-136">이 시나리오에서는 *rdp-rule*입니다.</span><span class="sxs-lookup"><span data-stu-id="77078-136">For our scenario, *rdp-rule*.</span></span>
   * <span data-ttu-id="77078-137">**-c(또는 --access)**.</span><span class="sxs-lookup"><span data-stu-id="77078-137">**-c (or --access)**.</span></span> <span data-ttu-id="77078-138">Hello 규칙 (Deny 또는 허용)에 대 한 액세스 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="77078-138">Access level for hello rule (Deny or Allow).</span></span>
   * <span data-ttu-id="77078-139">**-p(또는 --protocol)**.</span><span class="sxs-lookup"><span data-stu-id="77078-139">**-p (or --protocol)**.</span></span> <span data-ttu-id="77078-140">프로토콜 (Tcp, Udp 또는 *) hello 규칙에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="77078-140">Protocol (Tcp, Udp, or *) for hello rule.</span></span>
   * <span data-ttu-id="77078-141">**-r(또는 --direction)**.</span><span class="sxs-lookup"><span data-stu-id="77078-141">**-r (or --direction)**.</span></span> <span data-ttu-id="77078-142">연결 방향(인바운드 또는 아웃바운드)입니다.</span><span class="sxs-lookup"><span data-stu-id="77078-142">Direction of connection (Inbound or Outbound).</span></span>
   * <span data-ttu-id="77078-143">**-y(또는 --priority)**.</span><span class="sxs-lookup"><span data-stu-id="77078-143">**-y (or --priority)**.</span></span> <span data-ttu-id="77078-144">Hello 규칙에 대 한 우선 순위입니다.</span><span class="sxs-lookup"><span data-stu-id="77078-144">Priority for hello rule.</span></span>
   * <span data-ttu-id="77078-145">**-f(또는 --source-address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="77078-145">**-f (or --source-address-prefix)**.</span></span> <span data-ttu-id="77078-146">CIDR 또는 기본 태그를 사용하는 원본 주소 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="77078-146">Source address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="77078-147">**-o(또는 --source-port-range)**.</span><span class="sxs-lookup"><span data-stu-id="77078-147">**-o (or --source-port-range)**.</span></span> <span data-ttu-id="77078-148">원본 포트 또는 포트 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="77078-148">Source port, or port range.</span></span>
   * <span data-ttu-id="77078-149">**-e(또는 --destination-address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="77078-149">**-e (or --destination-address-prefix)**.</span></span> <span data-ttu-id="77078-150">CIDR 또는 기본 태그를 사용하는 대상 주소 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="77078-150">Destination address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="77078-151">**-u(또는 --destination-port-range)**.</span><span class="sxs-lookup"><span data-stu-id="77078-151">**-u (or --destination-port-range)**.</span></span> <span data-ttu-id="77078-152">대상 포트 또는 포트 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="77078-152">Destination port, or port range.</span></span>    
5. <span data-ttu-id="77078-153">Hello 실행 **azure 네트워크 nsg 규칙 만들기** 명령 toocreate hello 인터넷에서에서 액세스 tooport 80 (HTTP)를 허용 하는 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="77078-153">Run hello **azure network nsg rule create** command toocreate a rule that allows access tooport 80 (HTTP) from hello Internet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    <span data-ttu-id="77078-154">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="77078-154">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security rule "web-rule"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule
        data:    Name                            : web-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : Internet
        data:    Source Port                     : *
        data:    Destination IP                  : *
        data:    Destination Port                : 80
        data:    Protocol                        : Tcp
        data:    Direction                       : Inbound
        data:    Access                          : Allow
        data:    Priority                        : 200
        info:    network nsg rule create command OK
6. <span data-ttu-id="77078-155">Hello 실행 **azure 네트워크 vnet 서브넷 집합** 명령 toolink hello NSG toohello 프런트 엔드 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="77078-155">Run hello **azure network vnet subnet set** command toolink hello NSG toohello front end subnet.</span></span>
   
        azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -o NSG-FrontEnd
   
    <span data-ttu-id="77078-156">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="77078-156">Expected output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:    Network security group          : [object Object]
        data:    IP configurations:
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ip
        Configurations/ipconfig1
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ip
        Configurations/ipconfig1
        data:    
        info:    network vnet subnet set command OK

## <a name="how-toocreate-hello-nsg-for-hello-back-end-subnet"></a><span data-ttu-id="77078-157">Toocreate hello NSG 다시 hello에 대 한 서브넷을 종료 하는 방법</span><span class="sxs-lookup"><span data-stu-id="77078-157">How toocreate hello NSG for hello back end subnet</span></span>
<span data-ttu-id="77078-158">명명 된 NSG 라는 toocreate *NSG 백 엔드* 아래 hello 단계에 따라 위의 hello 시나리오에 따라, 합니다.</span><span class="sxs-lookup"><span data-stu-id="77078-158">toocreate an NSG named named *NSG-BackEnd* based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="77078-159">Hello 실행 **azure 네트워크 nsg 만들기** 명령 toocreate NSG 합니다.</span><span class="sxs-lookup"><span data-stu-id="77078-159">Run hello **azure network nsg create** command toocreate an NSG.</span></span>
   
        azure network nsg create -g TestRG -l westus -n NSG-BackEnd
   
    <span data-ttu-id="77078-160">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="77078-160">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-BackEnd
        data:    Name                            : NSG-BackEnd
        data:    Type                            : Microsoft.Network/networkSecurityGroups
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Security group rules:
        data:    Name                           Source IP          Source Port  Destination IP  Destination Port  Protocol  Direction  Access  Priority
        data:    -----------------------------  -----------------  -----------  --------------  ----------------  --------  ---------  ------  --------
        data:    AllowVnetInBound               VirtualNetwork     *            VirtualNetwork  *                 *         Inbound    Allow   65000   
        data:    AllowAzureLoadBalancerInBound  AzureLoadBalancer  *            *               *                 *         Inbound    Allow   65001   
        data:    DenyAllInBound                 *                  *            *               *                 *         Inbound    Deny    65500   
        data:    AllowVnetOutBound              VirtualNetwork     *            VirtualNetwork  *                 *         Outbound   Allow   65000   
        data:    AllowInternetOutBound          *                  *            Internet        *                 *         Outbound   Allow   65001   
        data:    DenyAllOutBound                *                  *            *               *                 *         Outbound   Deny    65500   
        info:    network nsg create command OK
2. <span data-ttu-id="77078-161">Hello 실행 **azure 네트워크 nsg 규칙 만들기** 명령 toocreate hello 프런트 엔드 서브넷의 액세스 tooport 1433 (SQL)를 허용 하는 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="77078-161">Run hello **azure network nsg rule create** command toocreate a rule that allows access tooport 1433 (SQL) from hello front end subnet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    <span data-ttu-id="77078-162">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="77078-162">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security rule "sql-rule"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-BackEnd/securityRules/sql-rule
        data:    Name                            : sql-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : 192.168.1.0/24
        data:    Source Port                     : *
        data:    Destination IP                  : *
        data:    Destination Port                : 1433
        data:    Protocol                        : Tcp
        data:    Direction                       : Inbound
        data:    Access                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
3. <span data-ttu-id="77078-163">Hello 실행 **azure 네트워크 nsg 규칙 만들기** 명령 toocreate 액세스 toohello 인터넷 거부 하는 규칙에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="77078-163">Run hello **azure network nsg rule create** command toocreate a rule that denies access toohello Internet from.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-BackEnd -n web-rule -c Deny -p * -r Outbound -y 200 -f * -o * -e Internet -u *
   
    <span data-ttu-id="77078-164">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="77078-164">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security rule "web-rule"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-BackEnd/securityRules/web-rule
        data:    Name                            : web-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : *
        data:    Source Port                     : *
        data:    Destination IP                  : Internet
        data:    Destination Port                : *
        data:    Protocol                        : *
        data:    Direction                       : Outbound
        data:    Access                          : Deny
        data:    Priority                        : 200
        info:    network nsg rule create command OK
4. <span data-ttu-id="77078-165">Hello 실행 **azure 네트워크 vnet 서브넷 집합** 명령 toolink hello NSG toohello 다시 서브넷을 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="77078-165">Run hello **azure network vnet subnet set** command toolink hello NSG toohello back end subnet.</span></span>
   
        azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -o NSG-BackEnd
   
    <span data-ttu-id="77078-166">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="77078-166">Expected output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up hello subnet "BackEnd"
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Setting subnet "BackEnd"
        info:    Looking up hello subnet "BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/BackEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : BackEnd
        data:    Address prefix                  : 192.168.2.0/24
        data:    Network security group          : [object Object]
        data:    IP configurations:
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICSQL1/ip
        Configurations/ipconfig1
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICSQL2/ip
        Configurations/ipconfig1
        data:    
        info:    network vnet subnet set command OK

