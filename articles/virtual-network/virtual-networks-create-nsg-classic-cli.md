---
title: "Azure CLI를 사용하여 클래식 모드에서 NSG를 만드는 방법 | Microsoft Docs"
description: "Azure CLI를 사용하여 클래식 모드에서 NSG를 만들고 배포하는 방법을 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: 17d98950-5fbb-4653-bef6-d822ab37541e
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: 115a1937a4c88ba2b986a40c84b1b759ed5e03b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-nsgs-classic-in-the-azure-cli"></a><span data-ttu-id="31155-103">Azure CLI에서 NSG(클래식)를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="31155-103">How to create NSGs (classic) in the Azure CLI</span></span>
[!INCLUDE [virtual-networks-create-nsg-selectors-classic-include](../../includes/virtual-networks-create-nsg-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="31155-104">이 문서에서는 클래식 배포 모델에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="31155-104">This article covers the classic deployment model.</span></span> <span data-ttu-id="31155-105">[리소스 관리자 배포 모델에서 NSG를 만들](virtual-networks-create-nsg-arm-cli.md)수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31155-105">You can also [create NSGs in the Resource Manager deployment model](virtual-networks-create-nsg-arm-cli.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="31155-106">아래 샘플 Azure CLI 명령에는 위의 시나리오를 기반으로 이미 만들어져 있는 단순한 환경이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="31155-106">The sample Azure CLI commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="31155-107">이 문서에 표시된 대로 명령을 실행하려는 경우 먼저 [VNet을 만들어](virtual-networks-create-vnet-classic-cli.md)테스트 환경을 구축합니다.</span><span class="sxs-lookup"><span data-stu-id="31155-107">If you want to run the commands as they are displayed in this document, first build the test environment by [creating a VNet](virtual-networks-create-vnet-classic-cli.md).</span></span>

## <a name="how-to-create-the-nsg-for-the-front-end-subnet"></a><span data-ttu-id="31155-108">프런트 엔드 서브넷에 대한 NSG를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="31155-108">How to create the NSG for the front end subnet</span></span>
<span data-ttu-id="31155-109">위의 시나리오에 따라 **NSG-FrontEnd** 라는 NSG를 만들려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="31155-109">To create an NSG named named **NSG-FrontEnd** based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="31155-110">Azure CLI를 처음 사용하는 경우 [Azure CLI 설치 및 구성](../cli-install-nodejs.md) 을 참조하고 Azure 계정 및 구독을 선택하는 부분까지 관련 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="31155-110">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="31155-111">아래와 같이 **`azure config mode`** 명령을 실행하여 클래식 모드로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="31155-111">Run the **`azure config mode`** command to switch to classic mode, as shown below.</span></span>
   
        azure config mode asm
   
    <span data-ttu-id="31155-112">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="31155-112">Expected output:</span></span>
   
        info:    New mode is asm
3. <span data-ttu-id="31155-113">**`azure network nsg create`** 명령을 실행하여 NSG를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31155-113">Run the **`azure network nsg create`** command to create an NSG.</span></span>
   
        azure network nsg create -l uswest -n NSG-FrontEnd
   
    <span data-ttu-id="31155-114">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="31155-114">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up the network security group "NSG-FrontEnd"
        data:    Name                            : NSG-FrontEnd
        data:    Location                        : West US
        data:    Security group rules:
        data:    Name                               Source IP           Source Port  Destination IP   Destination Port  Protocol  Type      Action  Prior
        ity  Default
        data:    ---------------------------------  ------------------  -----------  ---------------  ----------------  --------  --------  ------  -----
        ---  -------
        data:    ALLOW VNET OUTBOUND                VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Outbound  Allow   65000
             true   
        data:    ALLOW VNET INBOUND                 VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Inbound   Allow   65000
             true   
        data:    ALLOW AZURE LOAD BALANCER INBOUND  AZURE_LOADBALANCER  *            *                *                 *         Inbound   Allow   65001
             true   
        data:    ALLOW INTERNET OUTBOUND            *                   *            INTERNET         *                 *         Outbound  Allow   65001
             true   
        data:    DENY ALL OUTBOUND                  *                   *            *                *                 *         Outbound  Deny    65500
             true   
        data:    DENY ALL INBOUND                   *                   *            *                *                 *         Inbound   Deny    65500
             true   
        info:    network nsg create command OK
   
    <span data-ttu-id="31155-115">매개 변수</span><span class="sxs-lookup"><span data-stu-id="31155-115">Parameters:</span></span>
   
   * <span data-ttu-id="31155-116">**-l(또는 --location)**.</span><span class="sxs-lookup"><span data-stu-id="31155-116">**-l (or --location)**.</span></span> <span data-ttu-id="31155-117">새 NSG를 만들 Azure 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="31155-117">Azure region where the new NSG will be created.</span></span> <span data-ttu-id="31155-118">이 시나리오에서는 *westus*입니다.</span><span class="sxs-lookup"><span data-stu-id="31155-118">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="31155-119">**-n(또는 --name)**.</span><span class="sxs-lookup"><span data-stu-id="31155-119">**-n (or --name)**.</span></span> <span data-ttu-id="31155-120">새 NSG의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="31155-120">Name for the new NSG.</span></span> <span data-ttu-id="31155-121">이 시나리오에서는 *NSG-FrontEnd*입니다.</span><span class="sxs-lookup"><span data-stu-id="31155-121">For our scenario, *NSG-FrontEnd*.</span></span>
4. <span data-ttu-id="31155-122">**`azure network nsg rule create`** 명령을 실행하여 인터넷에서 포트 3389(RDP)에 대한 액세스를 허용하는 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31155-122">Run the **`azure network nsg rule create`** command to create a rule that allows access to port 3389 (RDP) from the Internet.</span></span>
   
        azure network nsg rule create -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    <span data-ttu-id="31155-123">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="31155-123">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security group "NSG-FrontEnd"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up the network security group "NSG-FrontEnd"
        data:    Name                            : rdp-rule
        data:    Source address prefix           : INTERNET
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 3389
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
   
    <span data-ttu-id="31155-124">매개 변수</span><span class="sxs-lookup"><span data-stu-id="31155-124">Parameters:</span></span>
   
   * <span data-ttu-id="31155-125">**-a(또는 --nsg-name)**.</span><span class="sxs-lookup"><span data-stu-id="31155-125">**-a (or --nsg-name)**.</span></span> <span data-ttu-id="31155-126">규칙이 만들어질 NSG의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="31155-126">Name of the NSG in which the rule will be created.</span></span> <span data-ttu-id="31155-127">이 시나리오에서는 *NSG-FrontEnd*입니다.</span><span class="sxs-lookup"><span data-stu-id="31155-127">For our scenario, *NSG-FrontEnd*.</span></span>
   * <span data-ttu-id="31155-128">**-n(또는 --name)**.</span><span class="sxs-lookup"><span data-stu-id="31155-128">**-n (or --name)**.</span></span> <span data-ttu-id="31155-129">새 규칙의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="31155-129">Name for the new rule.</span></span> <span data-ttu-id="31155-130">이 시나리오에서는 *rdp-rule*입니다.</span><span class="sxs-lookup"><span data-stu-id="31155-130">For our scenario, *rdp-rule*.</span></span>
   * <span data-ttu-id="31155-131">**-c(또는 --action)**.</span><span class="sxs-lookup"><span data-stu-id="31155-131">**-c (or --action)**.</span></span> <span data-ttu-id="31155-132">규칙(허용 또는 거부)에 대한 액세스 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="31155-132">Access level for the rule (Deny or Allow).</span></span>
   * <span data-ttu-id="31155-133">**-p(또는 --protocol)**.</span><span class="sxs-lookup"><span data-stu-id="31155-133">**-p (or --protocol)**.</span></span> <span data-ttu-id="31155-134">규칙에 대한 프로토콜(Tcp, Udp 또는 *)입니다.</span><span class="sxs-lookup"><span data-stu-id="31155-134">Protocol (Tcp, Udp, or *) for the rule.</span></span>
   * <span data-ttu-id="31155-135">**-r(또는 --type)**.</span><span class="sxs-lookup"><span data-stu-id="31155-135">**-r (or --type)**.</span></span> <span data-ttu-id="31155-136">연결 방향(인바운드 또는 아웃바운드)입니다.</span><span class="sxs-lookup"><span data-stu-id="31155-136">Direction of connection (Inbound or Outbound).</span></span>
   * <span data-ttu-id="31155-137">**-y(또는 --priority)**.</span><span class="sxs-lookup"><span data-stu-id="31155-137">**-y (or --priority)**.</span></span> <span data-ttu-id="31155-138">규칙에 대한 우선순위입니다.</span><span class="sxs-lookup"><span data-stu-id="31155-138">Priority for the rule.</span></span>
   * <span data-ttu-id="31155-139">**-f(또는 --source-address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="31155-139">**-f (or --source-address-prefix)**.</span></span> <span data-ttu-id="31155-140">CIDR 또는 기본 태그를 사용하는 원본 주소 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="31155-140">Source address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="31155-141">**-o(또는 --source-port-range)**.</span><span class="sxs-lookup"><span data-stu-id="31155-141">**-o (or --source-port-range)**.</span></span> <span data-ttu-id="31155-142">원본 포트 또는 포트 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="31155-142">Source port, or port range.</span></span>
   * <span data-ttu-id="31155-143">**-e(또는 --destination-address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="31155-143">**-e (or --destination-address-prefix)**.</span></span> <span data-ttu-id="31155-144">CIDR 또는 기본 태그를 사용하는 대상 주소 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="31155-144">Destination address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="31155-145">**-u(또는 --destination-port-range)**.</span><span class="sxs-lookup"><span data-stu-id="31155-145">**-u (or --destination-port-range)**.</span></span> <span data-ttu-id="31155-146">대상 포트 또는 포트 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="31155-146">Destination port, or port range.</span></span>
5. <span data-ttu-id="31155-147">**`azure network nsg rule create`** 명령을 실행하여 인터넷에서 포트 80(HTTP)에 대한 액세스를 허용하는 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31155-147">Run the **`azure network nsg rule create`** command to create a rule that allows access to port 80 (HTTP) from the Internet.</span></span>
   
        azure network nsg rule create -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    <span data-ttu-id="31155-148">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="31155-148">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security group "NSG-FrontEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up the network security group "NSG-FrontEnd"
        data:    Name                            : web-rule
        data:    Source address prefix           : INTERNET
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 80
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 200
        info:    network nsg rule create command OK
6. <span data-ttu-id="31155-149">**`azure network nsg subnet add`** 명령을 실행하여 NSG를 프런트 엔드 서브넷에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="31155-149">Run the **`azure network nsg subnet add`** command to link the NSG to the front end subnet.</span></span>
   
        azure network nsg subnet add -a NSG-FrontEnd --vnet-name TestVNet --subnet-name FrontEnd
   
    <span data-ttu-id="31155-150">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="31155-150">Expected output:</span></span>
   
        info:    Executing command network nsg subnet add
        info:    Looking up the network security group "NSG-FrontEnd"
        info:    Looking up the subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-FrontEnd"
        info:    network nsg subnet add command OK

## <a name="how-to-create-the-nsg-for-the-back-end-subnet"></a><span data-ttu-id="31155-151">백 엔드 서브넷에 대한 NSG를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="31155-151">How to create the NSG for the back end subnet</span></span>
<span data-ttu-id="31155-152">위의 시나리오에 따라 *NSG-BackEnd* 라는 NSG를 만들려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="31155-152">To create an NSG named named *NSG-BackEnd* based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="31155-153">**`azure network nsg create`** 명령을 실행하여 NSG를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31155-153">Run the **`azure network nsg create`** command to create an NSG.</span></span>
   
        azure network nsg create -l uswest -n NSG-BackEnd
   
    <span data-ttu-id="31155-154">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="31155-154">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up the network security group "NSG-BackEnd"
        data:    Name                            : NSG-BackEnd
        data:    Location                        : West US
        data:    Security group rules:
        data:    Name                               Source IP           Source Port  Destination IP   Destination Port  Protocol  Type      Action  Prior
        ity  Default
        data:    ---------------------------------  ------------------  -----------  ---------------  ----------------  --------  --------  ------  -----
        ---  -------
        data:    ALLOW VNET OUTBOUND                VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Outbound  Allow   65000
             true   
        data:    ALLOW VNET INBOUND                 VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Inbound   Allow   65000
             true   
        data:    ALLOW AZURE LOAD BALANCER INBOUND  AZURE_LOADBALANCER  *            *                *                 *         Inbound   Allow   65001
             true   
        data:    ALLOW INTERNET OUTBOUND            *                   *            INTERNET         *                 *         Outbound  Allow   65001
             true   
        data:    DENY ALL OUTBOUND                  *                   *            *                *                 *         Outbound  Deny    65500
             true   
        data:    DENY ALL INBOUND                   *                   *            *                *                 *         Inbound   Deny    65500
             true   
        info:    network nsg create command OK
   
    <span data-ttu-id="31155-155">매개 변수</span><span class="sxs-lookup"><span data-stu-id="31155-155">Parameters:</span></span>
   
   * <span data-ttu-id="31155-156">**-l(또는 --location)**.</span><span class="sxs-lookup"><span data-stu-id="31155-156">**-l (or --location)**.</span></span> <span data-ttu-id="31155-157">새 NSG를 만들 Azure 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="31155-157">Azure region where the new NSG will be created.</span></span> <span data-ttu-id="31155-158">이 시나리오에서는 *westus*입니다.</span><span class="sxs-lookup"><span data-stu-id="31155-158">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="31155-159">**-n(또는 --name)**.</span><span class="sxs-lookup"><span data-stu-id="31155-159">**-n (or --name)**.</span></span> <span data-ttu-id="31155-160">새 NSG의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="31155-160">Name for the new NSG.</span></span> <span data-ttu-id="31155-161">이 시나리오에서는 *NSG-FrontEnd*입니다.</span><span class="sxs-lookup"><span data-stu-id="31155-161">For our scenario, *NSG-FrontEnd*.</span></span>
2. <span data-ttu-id="31155-162">**`azure network nsg rule create`** 명령을 실행하여 프런트 엔드 서브넷에서 포트 1433(SQL)에 대한 액세스를 허용하는 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31155-162">Run the **`azure network nsg rule create`** command to create a rule that allows access to port 1433 (SQL) from the front end subnet.</span></span>
   
        azure network nsg rule create -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    <span data-ttu-id="31155-163">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="31155-163">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security group "NSG-BackEnd"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up the network security group "NSG-BackEnd"
        data:    Name                            : sql-rule
        data:    Source address prefix           : 192.168.1.0/24
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 1433
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
3. <span data-ttu-id="31155-164">**`azure network nsg rule create`** 명령을 실행하여 인터넷으로 액세스를 거부하는 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31155-164">Run the **`azure network nsg rule create`** command to create a rule that denies access to the Internet.</span></span>
   
        azure network nsg rule create -a NSG-BackEnd -n web-rule -c Deny -p Tcp -r Outbound -y 200 -f * -o * -e Internet -u 80
   
    <span data-ttu-id="31155-165">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="31155-165">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security group "NSG-BackEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up the network security group "NSG-BackEnd"
        data:    Name                            : web-rule
        data:    Source address prefix           : *
        data:    Source Port                     : *
        data:    Destination address prefix      : INTERNET
        data:    Destination Port                : 80
        data:    Protocol                        : TCP
        data:    Type                            : Outbound
        data:    Action                          : Deny
        data:    Priority                        : 200
        info:    network nsg rule create command OK
4. <span data-ttu-id="31155-166">**`azure network nsg subnet add`** 명령을 실행하여 NSG를 백 엔드 서브넷에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="31155-166">Run the **`azure network nsg subnet add`** command to link the NSG to the back end subnet.</span></span>
   
        azure network nsg subnet add -a NSG-BackEnd --vnet-name TestVNet --subnet-name BackEnd
   
    <span data-ttu-id="31155-167">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="31155-167">Expected output:</span></span>
   
        info:    Executing command network nsg subnet add
        info:    Looking up the network security group "NSG-BackEndX"
        info:    Looking up the subnet "BackEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-BackEndX"
        info:    network nsg subnet add command OK

