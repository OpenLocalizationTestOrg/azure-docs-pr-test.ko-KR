---
title: "aaaCreate 인터넷 연결 부하 분산 장치-Azure CLI | Microsoft Docs"
description: "Toocreate는 인터넷 연결 부하 분산 장치에 리소스 관리자를 사용 하 여 Azure CLI hello 하는 방법에 대해 알아봅니다"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a8bcdd88-f94c-4537-8143-c710eaa86818
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: cadb5edb3b4a4e2f0813109d027eaafdc7ef7303
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-load-balancer-using-hello-azure-cli"></a><span data-ttu-id="86186-103">Hello Azure CLI를 사용 하 여 인터넷 부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="86186-103">Creating an internet load balancer using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="86186-104">포털</span><span class="sxs-lookup"><span data-stu-id="86186-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="86186-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="86186-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="86186-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="86186-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="86186-107">템플릿</span><span class="sxs-lookup"><span data-stu-id="86186-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="86186-108">이 문서에서는 hello 리소스 관리자 배포 모델에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="86186-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="86186-109">수도 있습니다 [toocreate 인터넷 연결 부하 분산 장치 클래식 배포를 사용 하는 방법에 대해 알아봅니다](load-balancer-get-started-internet-classic-portal.md)</span><span class="sxs-lookup"><span data-stu-id="86186-109">You can also [Learn how toocreate an Internet facing load balancer using classic deployment](load-balancer-get-started-internet-classic-portal.md)</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-hello-solution-using-hello-azure-cli"></a><span data-ttu-id="86186-110">Hello Azure CLI를 사용 하 여 hello 솔루션 배포</span><span class="sxs-lookup"><span data-stu-id="86186-110">Deploying hello solution using hello Azure CLI</span></span>

<span data-ttu-id="86186-111">단계를 수행 하는 hello toocreate 인터넷 연결 부하 분산 장치 CLI Azure 리소스 관리자를 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="86186-111">hello following steps show how toocreate an Internet facing load balancer using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="86186-112">Azure 리소스 관리자와 각 리소스를 만들고 개별적으로 구성한 다음 준비 toocreate 리소스.</span><span class="sxs-lookup"><span data-stu-id="86186-112">With Azure Resource Manager each resource is created and configured individually, then put together toocreate a resource.</span></span>

<span data-ttu-id="86186-113">만들고 해야 개체 toodeploy 부하 분산 장치 뒤 hello 구성:</span><span class="sxs-lookup"><span data-stu-id="86186-113">You must create and configure hello following objects toodeploy a load balancer:</span></span>

* <span data-ttu-id="86186-114">프런트 엔드 IP 구성 - 들어오는 네트워크 트래픽에 대한 공용 IP 주소를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="86186-114">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="86186-115">백 엔드 주소 풀-hello hello 부하 분산 장치에서 가상 컴퓨터 tooreceive 네트워크 트래픽에 대 한 Nic (네트워크 인터페이스)를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="86186-115">Back-end address pool - contains network interfaces (NICs) for hello virtual machines tooreceive network traffic from hello load balancer.</span></span>
* <span data-ttu-id="86186-116">부하 분산 규칙-hello 백 엔드 주소 풀의 부하 분산 장치 tooport hello에 공용 포트 매핑 규칙을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="86186-116">Load balancing rules - contains rules mapping a public port on hello load balancer tooport in hello back-end address pool.</span></span>
* <span data-ttu-id="86186-117">인바운드 NAT 규칙-hello hello 백 엔드 주소 풀에서 특정 가상 컴퓨터에 대 한 부하 분산 장치 tooa 포트에 공용 포트 매핑 규칙을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="86186-117">Inbound NAT rules - contains rules mapping a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool.</span></span>
* <span data-ttu-id="86186-118">프로브-hello 백 엔드 주소 풀에 있는 가상 컴퓨터 인스턴스의 사용 된 검색 toocheck 가용성 상태를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="86186-118">Probes - contains health probes used toocheck availability of virtual machines instances in hello back-end address pool.</span></span>

<span data-ttu-id="86186-119">자세한 내용은 [부하 분산 장치에 대한 Azure Resource Manager 지원](load-balancer-arm.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86186-119">For more information see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-cli-toouse-resource-manager"></a><span data-ttu-id="86186-120">CLI toouse 리소스 관리자 설정</span><span class="sxs-lookup"><span data-stu-id="86186-120">Set up CLI toouse Resource Manager</span></span>

1. <span data-ttu-id="86186-121">Azure CLI 처음 사용 하는 경우 참조 [설치 및 구성 hello Azure CLI](../cli-install-nodejs.md) Azure 계정 및 구독을 선택 하면 toohello 포인트 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="86186-121">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="86186-122">Hello 실행 **azure 구성 모드** 명령 tooswitch tooResource 관리자 모드에서는 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="86186-122">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
        azure config mode arm
    ```

    <span data-ttu-id="86186-123">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="86186-123">Expected output:</span></span>

        info:    New mode is arm

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a><span data-ttu-id="86186-124">가상 네트워크 및 hello 프런트 엔드 IP 풀에 대 한 공용 IP 주소 만들기</span><span class="sxs-lookup"><span data-stu-id="86186-124">Create a virtual network and a public IP address for hello front-end IP pool</span></span>

1. <span data-ttu-id="86186-125">명명 된 가상 네트워크 (VNet) 만들기 *NRPVnet* 라는 리소스 그룹을 사용 하 여 hello 미국 동부 위치에 *NRPRG*합니다.</span><span class="sxs-lookup"><span data-stu-id="86186-125">Create a virtual network (VNet) named *NRPVnet* in hello East US location using a resource group named *NRPRG*.</span></span>

    ```azurecli
        azure network vnet create NRPRG NRPVnet eastUS -a 10.0.0.0/16
    ```

    <span data-ttu-id="86186-126">*NRPVnet*에서 10.0.0.0/24의 CIDR 블록으로 *NRPVnetSubnet*이라는 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="86186-126">Create a subnet named *NRPVnetSubnet* with a CIDR block of 10.0.0.0/24 in *NRPVnet*.</span></span>

    ```azurecli
        azure network vnet subnet create NRPRG NRPVnet NRPVnetSubnet -a 10.0.0.0/24
    ```

2. <span data-ttu-id="86186-127">명명 된 공용 IP 주소 만들기 *NRPPublicIP* toobe DNS 이름 사용 하 여 프런트 엔드 IP 풀에서 사용 하는 *loadbalancernrp.eastus.cloudapp.azure.com*. 아래 hello 명령을 hello 정적 할당 형식을 사용 하 고 4 분의 유휴 시간 제한입니다.</span><span class="sxs-lookup"><span data-stu-id="86186-127">Create a public IP address named *NRPPublicIP* toobe used by a front-end IP pool with DNS name *loadbalancernrp.eastus.cloudapp.azure.com*. hello command below uses hello static allocation type and idle timeout of 4 minutes.</span></span>

    ```azurecli
        azure network public-ip create -g NRPRG -n NRPPublicIP -l eastus -d loadbalancernrp -a static -i 4
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="86186-128">hello 부하 분산 장치는 FQDN으로 hello 공용 IP의 도메인 레이블을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="86186-128">hello load balancer will use hello domain label of hello public IP as its FQDN.</span></span> <span data-ttu-id="86186-129">이 부하 분산 장치 정규화 된 도메인 이름 (FQDN) hello으로 hello 클라우드 서비스를 사용 하는 클래식 배포에서 변경 된 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="86186-129">This a change from classic deployment, which uses hello cloud service as hello load balancer Fully Qualified Domain Name (FQDN).</span></span>
   > <span data-ttu-id="86186-130">이 예제에서는 hello FQDN은 *loadbalancernrp.eastus.cloudapp.azure.com*합니다.</span><span class="sxs-lookup"><span data-stu-id="86186-130">In this example, hello FQDN is *loadbalancernrp.eastus.cloudapp.azure.com*.</span></span>

## <a name="create-a-load-balancer"></a><span data-ttu-id="86186-131">부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="86186-131">Create a load balancer</span></span>

<span data-ttu-id="86186-132">hello 다음 명령은 명명 된 부하 분산 장치 *NRPlb* hello에 *NRPRG* hello의 리소스 그룹 *미국 동부* 는 Azure 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="86186-132">hello following command creates a load balancer named *NRPlb* in hello *NRPRG* resource group in hello *East US* Azure location.</span></span>

    ```azurecli
    azure network lb create NRPRG NRPlb eastus
    ```

## <a name="create-a-front-end-ip-pool-and-a-backend-address-pool"></a><span data-ttu-id="86186-133">프런트 엔드 IP 풀 및 백 엔드 주소 풀 만들기</span><span class="sxs-lookup"><span data-stu-id="86186-133">Create a front-end IP pool and a backend address pool</span></span>
<span data-ttu-id="86186-134">이 방법을 보여 주는이 예제 toocreate hello 프런트 엔드 IP 풀을 hello hello 들어오는 네트워크 트래픽을 받는 부하 분산 장치 백 엔드 IP 풀 hello 프런트 엔드 풀에서 hello 부하 분산 된 네트워크 트래픽을 전송 하는 위치를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="86186-134">This example demonstrates how toocreate hello front-end IP pool that receives hello incoming network traffic on hello load balancer and hello backend IP pool where hello front-end pool sends hello load balanced network traffic.</span></span>

1. <span data-ttu-id="86186-135">Hello 부하 분산 장치 및 hello 이전 단계에서 만든 hello 공용 IP를 연결 하는 프런트 엔드 IP 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="86186-135">Create a front-end IP pool associating hello public IP created in hello previous step and hello load balancer.</span></span>

    ```azurecli
        azure network lb frontend-ip create nrpRG NRPlb NRPfrontendpool -i nrppublicip
    ```

2. <span data-ttu-id="86186-136">Tooreceive 들어오는 트래픽을 hello 프런트 엔드 IP 풀에서 사용 하는 백 엔드 주소 풀을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="86186-136">Set up a back-end address pool used tooreceive incoming traffic from hello front-end IP pool.</span></span>

    ```azurecli
        azure network lb address-pool create NRPRG NRPlb NRPbackendpool
    ```

## <a name="create-lb-rules-nat-rules-and-probe"></a><span data-ttu-id="86186-137">LB 규칙, NAT 규칙 및 프로브 만들기</span><span class="sxs-lookup"><span data-stu-id="86186-137">Create LB rules, NAT rules, and probe</span></span>

<span data-ttu-id="86186-138">이 예제는 hello 다음 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="86186-138">This example creates hello following items.</span></span>

* <span data-ttu-id="86186-139">NAT 규칙 tootranslate 포트 21 tooport 22에서 들어오는 모든 트래픽을<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="86186-139">a NAT rule tootranslate all incoming traffic on port 21 tooport 22<sup>1</sup></span></span>
* <span data-ttu-id="86186-140">NAT 규칙 tootranslate 포트 23 tooport 22에서 들어오는 모든 트래픽을</span><span class="sxs-lookup"><span data-stu-id="86186-140">a NAT rule tootranslate all incoming traffic on port 23 tooport 22</span></span>
* <span data-ttu-id="86186-141">부하 분산 장치 규칙 toobalance hello에 포트 80 tooport 80에 들어오는 모든 트래픽을 hello 백 엔드 풀에서 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="86186-141">a load balancer rule toobalance all incoming traffic on port 80 tooport 80 on hello addresses in hello back-end pool.</span></span>
* <span data-ttu-id="86186-142">명명 된 페이지에는 프로브 규칙 toocheck hello 상태 상태 *HealthProbe.aspx*합니다.</span><span class="sxs-lookup"><span data-stu-id="86186-142">a probe rule toocheck hello health status on a page named *HealthProbe.aspx*.</span></span>

<span data-ttu-id="86186-143"><sup>1</sup> NAT 규칙은 hello 부하 분산 장치 뒤에 있는 특정 가상 컴퓨터 인스턴스 관련된 tooa 합니다.</span><span class="sxs-lookup"><span data-stu-id="86186-143"><sup>1</sup> NAT rules are associated tooa specific virtual machine instance behind hello load balancer.</span></span> <span data-ttu-id="86186-144">21 포트에 도착 하는 hello 네트워크 트래픽은 22이 NAT 규칙와 연결 된 포트에서 tooa 특정 가상 컴퓨터를 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86186-144">hello network traffic arriving on port 21 is sent tooa specific virtual machine on port 22 associated with this NAT rule.</span></span> <span data-ttu-id="86186-145">NAT 규칙에 대한 프로토콜(UDP 또는 TCP)을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86186-145">You must specify a protocol (UDP or TCP) for a NAT rule.</span></span> <span data-ttu-id="86186-146">두 프로토콜을 모두 안 toohello 동일한 포트를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="86186-146">Both protocols can't be assigned toohello same port.</span></span>

1. <span data-ttu-id="86186-147">Hello NAT 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="86186-147">Create hello NAT rules.</span></span>

    ```azurecli
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh1 --protocol tcp --frontend-port 21 --backend-port 22
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh2 --protocol tcp --frontend-port 23 --backend-port 22
    ```

2. <span data-ttu-id="86186-148">부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="86186-148">Create a load balancer rule.</span></span>

    ```azurecli
        azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule --protocol tcp --frontend-port 80 --backend-port 80 --frontend-ip-name NRPfrontendpool --backend-address-pool-name NRPbackendpool
    ```

3. <span data-ttu-id="86186-149">상태 프로브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="86186-149">Create a health probe.</span></span>

    ```azurecli
        azure network lb probe create --resource-group nrprg --lb-name nrplb --name healthprobe --protocol "http" --port 80 --path healthprobe.aspx --interval 15 --count 4
    ```

4. <span data-ttu-id="86186-150">설정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="86186-150">Check your settings.</span></span>

    ```azurecli
        azure network lb show nrprg nrplb
    ```

    <span data-ttu-id="86186-151">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="86186-151">Expected output:</span></span>

        info:    Executing command network lb show
        + Looking up hello load balancer "nrplb"
        + Looking up hello public ip "NRPPublicIP"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb
        data:    Name                            : nrplb
        data:    Type                            : Microsoft.Network/loadBalancers
        data:    Location                        : eastus
        data:    Provisioning State              : Succeeded
        data:    Frontend IP configurations:
        data:      Name                          : NRPfrontendpool
        data:      Provisioning state            : Succeeded
        data:      Public IP address id          : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/publicIPAddresses/NRPPublicIP
        data:      Public IP allocation method   : Static
        data:      Public IP address             : 40.114.13.145
        data:
        data:    Backend address pools:
        data:      Name                          : NRPbackendpool
        data:      Provisioning state            : Succeeded
        data:
        data:    Load balancing rules:
        data:      Name                          : HTTP
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 80
        data:      Backend port                  : 80
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:      Backend address pool          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:
        data:    Inbound NAT rules:
        data:      Name                          : ssh1
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 21
        data:      Backend port                  : 22
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:
        data:      Name                          : ssh2
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 23
        data:      Backend port                  : 22
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:
        data:    Probes:
        data:      Name                          : healthprobe
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Http
        data:      Port                          : 80
        data:      Interval in seconds           : 15
        data:      Number of probes              : 4
        data:
        info:    network lb show command OK

## <a name="create-nics"></a><span data-ttu-id="86186-152">NIC 만들기</span><span class="sxs-lookup"><span data-stu-id="86186-152">Create NICs</span></span>

<span data-ttu-id="86186-153">Toocreate nic가 필요 (또는 기존 템플릿을 수정할)와 tooNAT 규칙, 부하 분산 장치 규칙 및 프로브에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="86186-153">You need toocreate NICs (or modify existing ones) and associate them tooNAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="86186-154">명명 된 NIC를 만들고 *lb nic1 수*, hello와 연결 *rdp1* NAT 규칙을 hello *NRPbackendpool* 백 엔드 주소 풀입니다.</span><span class="sxs-lookup"><span data-stu-id="86186-154">Create a NIC named *lb-nic1-be*, and associate it with hello *rdp1* NAT rule, and hello *NRPbackendpool* back-end address pool.</span></span>

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" eastus
    ```

    <span data-ttu-id="86186-155">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="86186-155">Expected output:</span></span>

        info:    Executing command network nic create
        + Looking up hello network interface "lb-nic1-be"
        + Looking up hello subnet "nrpvnetsubnet"
        + Creating network interface "lb-nic1-be"
        + Looking up hello network interface "lb-nic1-be"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        data:    Name                            : lb-nic1-be
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : eastus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 10.0.0.4
        data:      Private IP Allocation Method  : Dynamic
        data:      Subnet                        : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet
        data:      Load balancer backend address pools
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:      Load balancer inbound NAT rules:
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1
        data:
        info:    network nic create command OK

2. <span data-ttu-id="86186-156">명명 된 NIC를 만들고 *lb nic2 수*, hello와 연결 *rdp2* NAT 규칙을 hello *NRPbackendpool* 백 엔드 주소 풀입니다.</span><span class="sxs-lookup"><span data-stu-id="86186-156">Create a NIC named *lb-nic2-be*, and associate it with hello *rdp2* NAT rule, and hello *NRPbackendpool* back-end address pool.</span></span>

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" eastus
    ```

3. <span data-ttu-id="86186-157">라는 가상 컴퓨터 (VM) 만들기 *web1*, hello 라는 NIC에 연결할 *lb nic1 수*합니다.</span><span class="sxs-lookup"><span data-stu-id="86186-157">Create a virtual machine (VM) named *web1*, and associate it with hello NIC named *lb-nic1-be*.</span></span> <span data-ttu-id="86186-158">저장소 계정 이라는 *web1nrp* 아래 hello 명령을 실행 하기 전에 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="86186-158">A storage account called *web1nrp* was created before running hello command below.</span></span>

    ```azurecli
        azure vm create --resource-group nrprg --name web1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="86186-159">Vm에서 부하 분산 장치 필요 toobe에 hello 동일한 가용성 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="86186-159">VMs in a load balancer need toobe in hello same availability set.</span></span> <span data-ttu-id="86186-160">사용 하 여 `azure availset create` toocreate 한 가용성 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="86186-160">Use `azure availset create` toocreate an availability set.</span></span>

    <span data-ttu-id="86186-161">hello 출력은 비슷한 toohello 다음 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86186-161">hello output should be similar toohello following:</span></span>

        info:    Executing command vm create
        + Looking up hello VM "web1"
        Enter username: azureuser
        Enter password for azureuser: *********
        Confirm password: *********
        info:    Using hello VM Size "Standard_A1"
        info:    hello [OS, Data] Disk or image configuration requires storage account
        + Looking up hello storage account web1nrp
        + Looking up hello availability set "nrp-avset"
        info:    Found an Availability set "nrp-avset"
        + Looking up hello NIC "lb-nic1-be"
        info:    Found an existing NIC "lb-nic1-be"
        info:    Found an IP configuration with virtual network subnet id "/subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet" in hello NIC "lb-nic1-be"
        info:    This is a NIC without publicIP configured
        + Creating VM "web1"
        info:    vm create command OK

    > [!NOTE]
    > <span data-ttu-id="86186-162">hello 정보 메시지 **publicIP 구성 하지 않고 NIC 이것이** 만들어지므로 hello NIC tooInternet hello 부하 분산 장치 공용 IP 주소를 사용 하 여 연결 하는 hello 부하 분산 장치에 대 한 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="86186-162">hello informational message **This is a NIC without publicIP configured** is expected since hello NIC created for hello load balancer connecting tooInternet using hello load balancer public IP address.</span></span>

    <span data-ttu-id="86186-163">Hello 이후 *lb nic1 수* hello와 연결 된 NIC *rdp1* NAT 규칙을 너무 연결할 수 있습니다*web1* 3441 hello 부하 분산 장치에 포트를 통해 RDP를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="86186-163">Since hello *lb-nic1-be* NIC is associated with hello *rdp1* NAT rule, you can connect too*web1* using RDP through port 3441 on hello load balancer.</span></span>

4. <span data-ttu-id="86186-164">라는 가상 컴퓨터 (VM) 만들기 *web2*, hello 라는 NIC에 연결할 *lb nic2 수*합니다.</span><span class="sxs-lookup"><span data-stu-id="86186-164">Create a virtual machine (VM) named *web2*, and associate it with hello NIC named *lb-nic2-be*.</span></span> <span data-ttu-id="86186-165">저장소 계정 이라는 *web1nrp* 아래 hello 명령을 실행 하기 전에 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="86186-165">A storage account called *web1nrp* was created before running hello command below.</span></span>

    ```azurecli
        azure vm create --resource-group nrprg --name web2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="86186-166">기존 부하 분산 장치 업데이트</span><span class="sxs-lookup"><span data-stu-id="86186-166">Update an existing load balancer</span></span>
<span data-ttu-id="86186-167">기존 부하 분산 장치를 참조하는 규칙을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86186-167">You can add rules referencing an existing load balancer.</span></span> <span data-ttu-id="86186-168">Hello 다음 예제는 새 부하 분산 장치 규칙 tooan 기존 부하 분산 장치 추가 **NRPlb**</span><span class="sxs-lookup"><span data-stu-id="86186-168">In hello next example, a new load balancer rule is added tooan existing load balancer **NRPlb**</span></span>

```azurecli
azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule2 --protocol tcp --frontend-port 8080 --backend-port 8051 --frontend-ip-name frontendnrppool --backend-address-pool-name NRPbackendpool
```

## <a name="delete-a-load-balancer"></a><span data-ttu-id="86186-169">부하 분산 장치 삭제</span><span class="sxs-lookup"><span data-stu-id="86186-169">Delete a load balancer</span></span>
<span data-ttu-id="86186-170">명령 tooremove 부하 분산 장치 뒤 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="86186-170">Use hello following command tooremove a load balancer:</span></span>

```azurecli
azure network lb delete --resource-group nrprg --name nrplb
```

## <a name="next-steps"></a><span data-ttu-id="86186-171">다음 단계</span><span class="sxs-lookup"><span data-stu-id="86186-171">Next steps</span></span>
[<span data-ttu-id="86186-172">내부 부하 분산 장치 구성 시작</span><span class="sxs-lookup"><span data-stu-id="86186-172">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-cli.md)

[<span data-ttu-id="86186-173">부하 분산 장치 배포 모드 구성</span><span class="sxs-lookup"><span data-stu-id="86186-173">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="86186-174">부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성</span><span class="sxs-lookup"><span data-stu-id="86186-174">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
