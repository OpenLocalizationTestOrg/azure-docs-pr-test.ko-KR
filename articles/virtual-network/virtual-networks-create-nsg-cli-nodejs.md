---
title: "네트워크 보안 그룹 만들기 - Azure CLI 1.0 | Microsoft Docs"
description: "Azure CLI 1.0을 사용하여 네트워크 보안 그룹을 만들고 배포하는 방법을 알아봅니다."
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
ms.openlocfilehash: ca8c182651e3c9f2f1f3a85b94361755d8e638d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-network-security-groups-using-the-azure-cli-10"></a><span data-ttu-id="e96a4-103">Azure CLI 1.0을 사용하여 네트워크 보안 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="e96a4-103">Create network security groups using the Azure CLI 1.0</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="e96a4-104">태스크를 완료하기 위한 CLI 버전</span><span class="sxs-lookup"><span data-stu-id="e96a4-104">CLI versions to complete the task</span></span> 

<span data-ttu-id="e96a4-105">다음 CLI 버전 중 하나를 사용하여 태스크를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e96a4-105">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="e96a4-106">[Azure CLI 1.0](#how-to-create-the-nsg-for-the-front-end-subnet) - 클래식 및 리소스 관리 배포 모델용 CLI(이 문서)</span><span class="sxs-lookup"><span data-stu-id="e96a4-106">[Azure CLI 1.0](#how-to-create-the-nsg-for-the-front-end-subnet) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="e96a4-107">[Azure CLI 2.0](virtual-networks-create-nsg-arm-cli.md) - 리소스 관리 배포 모델용 차세대 CLI</span><span class="sxs-lookup"><span data-stu-id="e96a4-107">[Azure CLI 2.0](virtual-networks-create-nsg-arm-cli.md) - our next-generation CLI for the resource management deployment model</span></span> 

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="e96a4-108">이 문서에서는 리소스 관리자 배포 모델에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e96a4-108">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="e96a4-109">[클래식 배포 모델에서 NSG를 만들](virtual-networks-create-nsg-classic-cli.md)수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e96a4-109">You can also [create NSGs in the classic deployment model](virtual-networks-create-nsg-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="e96a4-110">아래 샘플 Azure CLI 명령에는 위의 시나리오를 기반으로 이미 만들어져 있는 단순한 환경이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e96a4-110">The sample Azure CLI commands below expect a simple environment already created based on the scenario above.</span></span> 

## <a name="how-to-create-the-nsg-for-the-front-end-subnet"></a><span data-ttu-id="e96a4-111">프런트 엔드 서브넷에 대한 NSG를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="e96a4-111">How to create the NSG for the front end subnet</span></span>
<span data-ttu-id="e96a4-112">위의 시나리오에 따라 *NSG-FrontEnd* 라는 NSG를 만들려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="e96a4-112">To create an NSG named named *NSG-FrontEnd* based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="e96a4-113">Azure CLI를 처음 사용하는 경우 [Azure CLI 설치 및 구성](../cli-install-nodejs.md) 을 참조하고 Azure 계정 및 구독을 선택하는 부분까지 관련 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="e96a4-113">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="e96a4-114">아래와 같이 **azure config mode** 명령을 실행하여 리소스 관리자 모드로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="e96a4-114">Run the **azure config mode** command to switch to Resource Manager mode, as shown below.</span></span>
   
        azure config mode arm
   
    <span data-ttu-id="e96a4-115">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="e96a4-115">Expected output:</span></span>
   
        info:    New mode is arm
3. <span data-ttu-id="e96a4-116">**azure network nsg create** 명령을 실행하여 NSG를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e96a4-116">Run the **azure network nsg create** command to create an NSG.</span></span>
   
        azure network nsg create -g TestRG -l westus -n NSG-FrontEnd
   
    <span data-ttu-id="e96a4-117">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="e96a4-117">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Looking up the network security group "NSG-FrontEnd"
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up the network security group "NSG-FrontEnd"
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
   
    <span data-ttu-id="e96a4-118">매개 변수</span><span class="sxs-lookup"><span data-stu-id="e96a4-118">Parameters:</span></span>
   
   * <span data-ttu-id="e96a4-119">**-g(또는 --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="e96a4-119">**-g (or --resource-group)**.</span></span> <span data-ttu-id="e96a4-120">NSG가 만들어지는 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e96a4-120">Name of the resource group where the NSG will be created.</span></span> <span data-ttu-id="e96a4-121">이 시나리오에서는 *TestRG*입니다.</span><span class="sxs-lookup"><span data-stu-id="e96a4-121">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="e96a4-122">**-l(또는 --location)**.</span><span class="sxs-lookup"><span data-stu-id="e96a4-122">**-l (or --location)**.</span></span> <span data-ttu-id="e96a4-123">새 NSG를 만들 Azure 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="e96a4-123">Azure region where the new NSG will be created.</span></span> <span data-ttu-id="e96a4-124">이 시나리오에서는 *westus*입니다.</span><span class="sxs-lookup"><span data-stu-id="e96a4-124">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="e96a4-125">**-n(또는 --name)**.</span><span class="sxs-lookup"><span data-stu-id="e96a4-125">**-n (or --name)**.</span></span> <span data-ttu-id="e96a4-126">새 NSG의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e96a4-126">Name for the new NSG.</span></span> <span data-ttu-id="e96a4-127">이 시나리오에서는 *NSG-FrontEnd*입니다.</span><span class="sxs-lookup"><span data-stu-id="e96a4-127">For our scenario, *NSG-FrontEnd*.</span></span>
4. <span data-ttu-id="e96a4-128">**azure network nsg rule create** 명령을 실행하여 인터넷에서 포트 3389(RDP)에 대한 액세스를 허용하는 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e96a4-128">Run the **azure network nsg rule create** command to create a rule that allows access to port 3389 (RDP) from the Internet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    <span data-ttu-id="e96a4-129">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="e96a4-129">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        warn:    Using default direction: Inbound
        info:    Looking up the network security rule "rdp-rule"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up the network security group "NSG-FrontEnd"
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
   
    <span data-ttu-id="e96a4-130">매개 변수</span><span class="sxs-lookup"><span data-stu-id="e96a4-130">Parameters:</span></span>
   
   * <span data-ttu-id="e96a4-131">**-a(또는 --nsg-name)**.</span><span class="sxs-lookup"><span data-stu-id="e96a4-131">**-a (or --nsg-name)**.</span></span> <span data-ttu-id="e96a4-132">규칙이 만들어질 NSG의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e96a4-132">Name of the NSG in which the rule will be created.</span></span> <span data-ttu-id="e96a4-133">이 시나리오에서는 *NSG-FrontEnd*입니다.</span><span class="sxs-lookup"><span data-stu-id="e96a4-133">For our scenario, *NSG-FrontEnd*.</span></span>
   * <span data-ttu-id="e96a4-134">**-n(또는 --name)**.</span><span class="sxs-lookup"><span data-stu-id="e96a4-134">**-n (or --name)**.</span></span> <span data-ttu-id="e96a4-135">새 규칙의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e96a4-135">Name for the new rule.</span></span> <span data-ttu-id="e96a4-136">이 시나리오에서는 *rdp-rule*입니다.</span><span class="sxs-lookup"><span data-stu-id="e96a4-136">For our scenario, *rdp-rule*.</span></span>
   * <span data-ttu-id="e96a4-137">**-c(또는 --access)**.</span><span class="sxs-lookup"><span data-stu-id="e96a4-137">**-c (or --access)**.</span></span> <span data-ttu-id="e96a4-138">규칙(허용 또는 거부)에 대한 액세스 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="e96a4-138">Access level for the rule (Deny or Allow).</span></span>
   * <span data-ttu-id="e96a4-139">**-p(또는 --protocol)**.</span><span class="sxs-lookup"><span data-stu-id="e96a4-139">**-p (or --protocol)**.</span></span> <span data-ttu-id="e96a4-140">규칙에 대한 프로토콜(Tcp, Udp 또는 *)입니다.</span><span class="sxs-lookup"><span data-stu-id="e96a4-140">Protocol (Tcp, Udp, or *) for the rule.</span></span>
   * <span data-ttu-id="e96a4-141">**-r(또는 --direction)**.</span><span class="sxs-lookup"><span data-stu-id="e96a4-141">**-r (or --direction)**.</span></span> <span data-ttu-id="e96a4-142">연결 방향(인바운드 또는 아웃바운드)입니다.</span><span class="sxs-lookup"><span data-stu-id="e96a4-142">Direction of connection (Inbound or Outbound).</span></span>
   * <span data-ttu-id="e96a4-143">**-y(또는 --priority)**.</span><span class="sxs-lookup"><span data-stu-id="e96a4-143">**-y (or --priority)**.</span></span> <span data-ttu-id="e96a4-144">규칙에 대한 우선순위입니다.</span><span class="sxs-lookup"><span data-stu-id="e96a4-144">Priority for the rule.</span></span>
   * <span data-ttu-id="e96a4-145">**-f(또는 --source-address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="e96a4-145">**-f (or --source-address-prefix)**.</span></span> <span data-ttu-id="e96a4-146">CIDR 또는 기본 태그를 사용하는 원본 주소 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="e96a4-146">Source address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="e96a4-147">**-o(또는 --source-port-range)**.</span><span class="sxs-lookup"><span data-stu-id="e96a4-147">**-o (or --source-port-range)**.</span></span> <span data-ttu-id="e96a4-148">원본 포트 또는 포트 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="e96a4-148">Source port, or port range.</span></span>
   * <span data-ttu-id="e96a4-149">**-e(또는 --destination-address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="e96a4-149">**-e (or --destination-address-prefix)**.</span></span> <span data-ttu-id="e96a4-150">CIDR 또는 기본 태그를 사용하는 대상 주소 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="e96a4-150">Destination address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="e96a4-151">**-u(또는 --destination-port-range)**.</span><span class="sxs-lookup"><span data-stu-id="e96a4-151">**-u (or --destination-port-range)**.</span></span> <span data-ttu-id="e96a4-152">대상 포트 또는 포트 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="e96a4-152">Destination port, or port range.</span></span>    
5. <span data-ttu-id="e96a4-153">**azure network nsg rule create** 명령을 실행하여 인터넷에서 포트 80(HTTP)에 대한 액세스를 허용하는 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e96a4-153">Run the **azure network nsg rule create** command to create a rule that allows access to port 80 (HTTP) from the Internet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    <span data-ttu-id="e96a4-154">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="e96a4-154">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security rule "web-rule"
        info:    Creating a network security rule "web-rule"
        info:    Looking up the network security group "NSG-FrontEnd"
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
6. <span data-ttu-id="e96a4-155">**azure network vnet subnet set** 명령을 실행하여 NSG를 프런트 엔드 서브넷에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e96a4-155">Run the **azure network vnet subnet set** command to link the NSG to the front end subnet.</span></span>
   
        azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -o NSG-FrontEnd
   
    <span data-ttu-id="e96a4-156">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="e96a4-156">Expected output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up the subnet "FrontEnd"
        info:    Looking up the network security group "NSG-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up the subnet "FrontEnd"
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

## <a name="how-to-create-the-nsg-for-the-back-end-subnet"></a><span data-ttu-id="e96a4-157">백 엔드 서브넷에 대한 NSG를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="e96a4-157">How to create the NSG for the back end subnet</span></span>
<span data-ttu-id="e96a4-158">위의 시나리오에 따라 *NSG-BackEnd* 라는 NSG를 만들려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="e96a4-158">To create an NSG named named *NSG-BackEnd* based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="e96a4-159">**azure network nsg create** 명령을 실행하여 NSG를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e96a4-159">Run the **azure network nsg create** command to create an NSG.</span></span>
   
        azure network nsg create -g TestRG -l westus -n NSG-BackEnd
   
    <span data-ttu-id="e96a4-160">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="e96a4-160">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Looking up the network security group "NSG-BackEnd"
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up the network security group "NSG-BackEnd"
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
2. <span data-ttu-id="e96a4-161">**azure network nsg rule create** 명령을 실행하여 프런트 엔드 서브넷에서 포트 1433(SQL)에 대한 액세스를 허용하는 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e96a4-161">Run the **azure network nsg rule create** command to create a rule that allows access to port 1433 (SQL) from the front end subnet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    <span data-ttu-id="e96a4-162">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="e96a4-162">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security rule "sql-rule"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up the network security group "NSG-BackEnd"
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
3. <span data-ttu-id="e96a4-163">**azure network nsg rule create** 명령을 실행하여 인터넷으로 액세스를 거부하는 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e96a4-163">Run the **azure network nsg rule create** command to create a rule that denies access to the Internet from.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-BackEnd -n web-rule -c Deny -p * -r Outbound -y 200 -f * -o * -e Internet -u *
   
    <span data-ttu-id="e96a4-164">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="e96a4-164">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security rule "web-rule"
        info:    Creating a network security rule "web-rule"
        info:    Looking up the network security group "NSG-BackEnd"
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
4. <span data-ttu-id="e96a4-165">**azure network vnet subnet set** 명령을 실행하여 NSG를 백 엔드 서브넷에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e96a4-165">Run the **azure network vnet subnet set** command to link the NSG to the back end subnet.</span></span>
   
        azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -o NSG-BackEnd
   
    <span data-ttu-id="e96a4-166">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="e96a4-166">Expected output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up the subnet "BackEnd"
        info:    Looking up the network security group "NSG-BackEnd"
        info:    Setting subnet "BackEnd"
        info:    Looking up the subnet "BackEnd"
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

