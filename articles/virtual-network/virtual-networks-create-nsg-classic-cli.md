---
title: "사용 하 여 클래식 모드로 aaaHow toocreate Nsg hello Azure CLI | Microsoft Docs"
description: "자세한 내용은 방법 toocreate hello Azure CLI를 사용 하 여 클래식 모드에서 Nsg를 배포 하 고"
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
ms.openlocfilehash: eb78861e10a0dd950bb2c3783ee957d1cce55016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-nsgs-classic-in-hello-azure-cli"></a><span data-ttu-id="1f759-103">Toocreate Nsg (클래식)를 Azure CLI hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1f759-103">How toocreate NSGs (classic) in hello Azure CLI</span></span>
[!INCLUDE [virtual-networks-create-nsg-selectors-classic-include](../../includes/virtual-networks-create-nsg-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="1f759-104">이 문서에서는 hello 클래식 배포 모델에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f759-104">This article covers hello classic deployment model.</span></span> <span data-ttu-id="1f759-105">수도 있습니다 [hello 리소스 관리자 배포 모델에서 Nsg 만들기](virtual-networks-create-nsg-arm-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1f759-105">You can also [create NSGs in hello Resource Manager deployment model](virtual-networks-create-nsg-arm-cli.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="1f759-106">hello 샘플 Azure CLI 명령 아래에 이미 위의 hello 시나리오를 기반으로 만들어진 단순 환경이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f759-106">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="1f759-107">이 문서에 표시 된 대로 toorun hello 명령을 원하는 경우 먼저 hello 테스트 환경을 구축 하 여 [VNet을 만드는](virtual-networks-create-vnet-classic-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1f759-107">If you want toorun hello commands as they are displayed in this document, first build hello test environment by [creating a VNet](virtual-networks-create-vnet-classic-cli.md).</span></span>

## <a name="how-toocreate-hello-nsg-for-hello-front-end-subnet"></a><span data-ttu-id="1f759-108">Toocreate NSG hello 프런트 엔드 서브넷에 대 한 hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1f759-108">How toocreate hello NSG for hello front end subnet</span></span>
<span data-ttu-id="1f759-109">명명 된 NSG 라는 toocreate **NSG 프런트 엔드** 아래 hello 단계에 따라 위의 hello 시나리오에 따라, 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f759-109">toocreate an NSG named named **NSG-FrontEnd** based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="1f759-110">Azure CLI 처음 사용 하는 경우 참조 [설치 및 구성 hello Azure CLI](../cli-install-nodejs.md) Azure 계정 및 구독을 선택 하면 toohello 포인트 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="1f759-110">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="1f759-111">Hello 실행  **`azure config mode`**  아래와 같이 명령 tooswitch tooclassic 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="1f759-111">Run hello **`azure config mode`** command tooswitch tooclassic mode, as shown below.</span></span>
   
        azure config mode asm
   
    <span data-ttu-id="1f759-112">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="1f759-112">Expected output:</span></span>
   
        info:    New mode is asm
3. <span data-ttu-id="1f759-113">Hello 실행  **`azure network nsg create`**  명령 toocreate NSG 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f759-113">Run hello **`azure network nsg create`** command toocreate an NSG.</span></span>
   
        azure network nsg create -l uswest -n NSG-FrontEnd
   
    <span data-ttu-id="1f759-114">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="1f759-114">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up hello network security group "NSG-FrontEnd"
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
   
    <span data-ttu-id="1f759-115">매개 변수</span><span class="sxs-lookup"><span data-stu-id="1f759-115">Parameters:</span></span>
   
   * <span data-ttu-id="1f759-116">**-l(또는 --location)**.</span><span class="sxs-lookup"><span data-stu-id="1f759-116">**-l (or --location)**.</span></span> <span data-ttu-id="1f759-117">Azure 지역 hello 새 NSG를 만들 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="1f759-117">Azure region where hello new NSG will be created.</span></span> <span data-ttu-id="1f759-118">이 시나리오에서는 *westus*입니다.</span><span class="sxs-lookup"><span data-stu-id="1f759-118">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="1f759-119">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="1f759-119">**-n (or --name)**.</span></span> <span data-ttu-id="1f759-120">Hello에 대 한 이름을 새 NSG 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f759-120">Name for hello new NSG.</span></span> <span data-ttu-id="1f759-121">이 시나리오에서는 *NSG-FrontEnd*입니다.</span><span class="sxs-lookup"><span data-stu-id="1f759-121">For our scenario, *NSG-FrontEnd*.</span></span>
4. <span data-ttu-id="1f759-122">Hello 실행  **`azure network nsg rule create`**  명령 toocreate hello 인터넷에서에서 액세스 tooport 3389 (RDP)를 허용 하는 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="1f759-122">Run hello **`azure network nsg rule create`** command toocreate a rule that allows access tooport 3389 (RDP) from hello Internet.</span></span>
   
        azure network nsg rule create -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    <span data-ttu-id="1f759-123">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="1f759-123">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
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
   
    <span data-ttu-id="1f759-124">매개 변수</span><span class="sxs-lookup"><span data-stu-id="1f759-124">Parameters:</span></span>
   
   * <span data-ttu-id="1f759-125">**-a(또는 --nsg-name)**.</span><span class="sxs-lookup"><span data-stu-id="1f759-125">**-a (or --nsg-name)**.</span></span> <span data-ttu-id="1f759-126">Hello NSG 규칙 만들 수 있는 hello의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1f759-126">Name of hello NSG in which hello rule will be created.</span></span> <span data-ttu-id="1f759-127">이 시나리오에서는 *NSG-FrontEnd*입니다.</span><span class="sxs-lookup"><span data-stu-id="1f759-127">For our scenario, *NSG-FrontEnd*.</span></span>
   * <span data-ttu-id="1f759-128">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="1f759-128">**-n (or --name)**.</span></span> <span data-ttu-id="1f759-129">Hello 새 규칙의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1f759-129">Name for hello new rule.</span></span> <span data-ttu-id="1f759-130">이 시나리오에서는 *rdp-rule*입니다.</span><span class="sxs-lookup"><span data-stu-id="1f759-130">For our scenario, *rdp-rule*.</span></span>
   * <span data-ttu-id="1f759-131">**-c(또는 --action)**.</span><span class="sxs-lookup"><span data-stu-id="1f759-131">**-c (or --action)**.</span></span> <span data-ttu-id="1f759-132">Hello 규칙 (Deny 또는 허용)에 대 한 액세스 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="1f759-132">Access level for hello rule (Deny or Allow).</span></span>
   * <span data-ttu-id="1f759-133">**-p(또는 --protocol)**.</span><span class="sxs-lookup"><span data-stu-id="1f759-133">**-p (or --protocol)**.</span></span> <span data-ttu-id="1f759-134">프로토콜 (Tcp, Udp 또는 *) hello 규칙에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f759-134">Protocol (Tcp, Udp, or *) for hello rule.</span></span>
   * <span data-ttu-id="1f759-135">**-r(또는 --type)**.</span><span class="sxs-lookup"><span data-stu-id="1f759-135">**-r (or --type)**.</span></span> <span data-ttu-id="1f759-136">연결 방향(인바운드 또는 아웃바운드)입니다.</span><span class="sxs-lookup"><span data-stu-id="1f759-136">Direction of connection (Inbound or Outbound).</span></span>
   * <span data-ttu-id="1f759-137">**-y(또는 --priority)**.</span><span class="sxs-lookup"><span data-stu-id="1f759-137">**-y (or --priority)**.</span></span> <span data-ttu-id="1f759-138">Hello 규칙에 대 한 우선 순위입니다.</span><span class="sxs-lookup"><span data-stu-id="1f759-138">Priority for hello rule.</span></span>
   * <span data-ttu-id="1f759-139">**-f(또는 --source-address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="1f759-139">**-f (or --source-address-prefix)**.</span></span> <span data-ttu-id="1f759-140">CIDR 또는 기본 태그를 사용하는 원본 주소 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="1f759-140">Source address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="1f759-141">**-o(또는 --source-port-range)**.</span><span class="sxs-lookup"><span data-stu-id="1f759-141">**-o (or --source-port-range)**.</span></span> <span data-ttu-id="1f759-142">원본 포트 또는 포트 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="1f759-142">Source port, or port range.</span></span>
   * <span data-ttu-id="1f759-143">**-e(또는 --destination-address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="1f759-143">**-e (or --destination-address-prefix)**.</span></span> <span data-ttu-id="1f759-144">CIDR 또는 기본 태그를 사용하는 대상 주소 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="1f759-144">Destination address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="1f759-145">**-u(또는 --destination-port-range)**.</span><span class="sxs-lookup"><span data-stu-id="1f759-145">**-u (or --destination-port-range)**.</span></span> <span data-ttu-id="1f759-146">대상 포트 또는 포트 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="1f759-146">Destination port, or port range.</span></span>
5. <span data-ttu-id="1f759-147">Hello 실행  **`azure network nsg rule create`**  명령 toocreate hello 인터넷에서에서 액세스 tooport 80 (HTTP)를 허용 하는 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="1f759-147">Run hello **`azure network nsg rule create`** command toocreate a rule that allows access tooport 80 (HTTP) from hello Internet.</span></span>
   
        azure network nsg rule create -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    <span data-ttu-id="1f759-148">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="1f759-148">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
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
6. <span data-ttu-id="1f759-149">Hello 실행  **`azure network nsg subnet add`**  명령 toolink hello NSG toohello 프런트 엔드 서브넷입니다.</span><span class="sxs-lookup"><span data-stu-id="1f759-149">Run hello **`azure network nsg subnet add`** command toolink hello NSG toohello front end subnet.</span></span>
   
        azure network nsg subnet add -a NSG-FrontEnd --vnet-name TestVNet --subnet-name FrontEnd
   
    <span data-ttu-id="1f759-150">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="1f759-150">Expected output:</span></span>
   
        info:    Executing command network nsg subnet add
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-FrontEnd"
        info:    network nsg subnet add command OK

## <a name="how-toocreate-hello-nsg-for-hello-back-end-subnet"></a><span data-ttu-id="1f759-151">Toocreate hello NSG 다시 hello에 대 한 서브넷을 종료 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1f759-151">How toocreate hello NSG for hello back end subnet</span></span>
<span data-ttu-id="1f759-152">명명 된 NSG 라는 toocreate *NSG 백 엔드* 아래 hello 단계에 따라 위의 hello 시나리오에 따라, 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f759-152">toocreate an NSG named named *NSG-BackEnd* based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="1f759-153">Hello 실행  **`azure network nsg create`**  명령 toocreate NSG 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f759-153">Run hello **`azure network nsg create`** command toocreate an NSG.</span></span>
   
        azure network nsg create -l uswest -n NSG-BackEnd
   
    <span data-ttu-id="1f759-154">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="1f759-154">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up hello network security group "NSG-BackEnd"
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
   
    <span data-ttu-id="1f759-155">매개 변수</span><span class="sxs-lookup"><span data-stu-id="1f759-155">Parameters:</span></span>
   
   * <span data-ttu-id="1f759-156">**-l(또는 --location)**.</span><span class="sxs-lookup"><span data-stu-id="1f759-156">**-l (or --location)**.</span></span> <span data-ttu-id="1f759-157">Azure 지역 hello 새 NSG를 만들 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="1f759-157">Azure region where hello new NSG will be created.</span></span> <span data-ttu-id="1f759-158">이 시나리오에서는 *westus*입니다.</span><span class="sxs-lookup"><span data-stu-id="1f759-158">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="1f759-159">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="1f759-159">**-n (or --name)**.</span></span> <span data-ttu-id="1f759-160">Hello에 대 한 이름을 새 NSG 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f759-160">Name for hello new NSG.</span></span> <span data-ttu-id="1f759-161">이 시나리오에서는 *NSG-FrontEnd*입니다.</span><span class="sxs-lookup"><span data-stu-id="1f759-161">For our scenario, *NSG-FrontEnd*.</span></span>
2. <span data-ttu-id="1f759-162">Hello 실행  **`azure network nsg rule create`**  명령 toocreate hello 프런트 엔드 서브넷의 액세스 tooport 1433 (SQL)를 허용 하는 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="1f759-162">Run hello **`azure network nsg rule create`** command toocreate a rule that allows access tooport 1433 (SQL) from hello front end subnet.</span></span>
   
        azure network nsg rule create -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    <span data-ttu-id="1f759-163">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="1f759-163">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
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
3. <span data-ttu-id="1f759-164">Hello 실행  **`azure network nsg rule create`**  명령 toocreate 액세스 toohello 인터넷 거부 하는 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="1f759-164">Run hello **`azure network nsg rule create`** command toocreate a rule that denies access toohello Internet.</span></span>
   
        azure network nsg rule create -a NSG-BackEnd -n web-rule -c Deny -p Tcp -r Outbound -y 200 -f * -o * -e Internet -u 80
   
    <span data-ttu-id="1f759-165">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="1f759-165">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
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
4. <span data-ttu-id="1f759-166">Hello 실행  **`azure network nsg subnet add`**  명령 toolink hello NSG toohello 다시 서브넷을 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f759-166">Run hello **`azure network nsg subnet add`** command toolink hello NSG toohello back end subnet.</span></span>
   
        azure network nsg subnet add -a NSG-BackEnd --vnet-name TestVNet --subnet-name BackEnd
   
    <span data-ttu-id="1f759-167">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="1f759-167">Expected output:</span></span>
   
        info:    Executing command network nsg subnet add
        info:    Looking up hello network security group "NSG-BackEndX"
        info:    Looking up hello subnet "BackEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-BackEndX"
        info:    network nsg subnet add command OK

