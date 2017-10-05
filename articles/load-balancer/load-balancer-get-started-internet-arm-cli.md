---
title: "인터넷 연결 부하 분산 장치 만들기 - Azure CLI | Microsoft Docs"
description: "Azure CLI를 사용하여 Resource Manager에서 인터넷 연결 부하 분산 장치를 만드는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 3b1780033cbc8aa3e108a213a4d2bfd0332fd7d7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="creating-an-internet-load-balancer-using-the-azure-cli"></a><span data-ttu-id="38460-103">Azure CLI를 사용하여 인터넷 부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="38460-103">Creating an internet load balancer using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="38460-104">포털</span><span class="sxs-lookup"><span data-stu-id="38460-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="38460-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="38460-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="38460-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="38460-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="38460-107">템플릿</span><span class="sxs-lookup"><span data-stu-id="38460-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="38460-108">이 문서에서는 리소스 관리자 배포 모델에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="38460-108">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="38460-109">또한 [클래식 배포를 사용하여 인터넷 연결 부하 분산 장치를 만드는 방법을 배울 수 있습니다](load-balancer-get-started-internet-classic-portal.md)</span><span class="sxs-lookup"><span data-stu-id="38460-109">You can also [Learn how to create an Internet facing load balancer using classic deployment](load-balancer-get-started-internet-classic-portal.md)</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-the-solution-using-the-azure-cli"></a><span data-ttu-id="38460-110">Azure CLI를 사용하여 솔루션 배포</span><span class="sxs-lookup"><span data-stu-id="38460-110">Deploying the solution using the Azure CLI</span></span>

<span data-ttu-id="38460-111">다음 단계에서는 CLI와 함께 Azure Resource Manager를 사용하여 인터넷 연결 부하 분산 장치를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="38460-111">The following steps show how to create an Internet facing load balancer using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="38460-112">Azure Resource Manager를 사용하면 각 리소스가 개별적으로 생성되고 구성된 다음, 함께 사용되어 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="38460-112">With Azure Resource Manager each resource is created and configured individually, then put together to create a resource.</span></span>

<span data-ttu-id="38460-113">부하 분산 장치를 배포하려면 다음 개체를 만들고 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="38460-113">You must create and configure the following objects to deploy a load balancer:</span></span>

* <span data-ttu-id="38460-114">프런트 엔드 IP 구성 - 들어오는 네트워크 트래픽에 대한 공용 IP 주소를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="38460-114">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="38460-115">백 엔드 주소 풀 - 부하 분산 장치의 네트워크 트래픽을 받는 가상 컴퓨터에 대한 NIC(네트워크 인터페이스)를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="38460-115">Back-end address pool - contains network interfaces (NICs) for the virtual machines to receive network traffic from the load balancer.</span></span>
* <span data-ttu-id="38460-116">부하 분산 규칙 - 백 엔드 주소 풀에 있는 포트에 부하 분산 장치의 공용 포트를 매핑하는 규칙을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="38460-116">Load balancing rules - contains rules mapping a public port on the load balancer to port in the back-end address pool.</span></span>
* <span data-ttu-id="38460-117">인바운드 NAT 규칙 - 백 엔드 주소 풀에 있는 특정 가상 컴퓨터에 대한 포트에 부하 분산 장치의 공용 포트를 매핑하는 규칙을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="38460-117">Inbound NAT rules - contains rules mapping a public port on the load balancer to a port for a specific virtual machine in the back-end address pool.</span></span>
* <span data-ttu-id="38460-118">프로브 - 백 엔드 주소 풀의 가상 컴퓨터 인스턴스의 가용성을 확인하는 데 사용하는 상태 프로브를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="38460-118">Probes - contains health probes used to check availability of virtual machines instances in the back-end address pool.</span></span>

<span data-ttu-id="38460-119">자세한 내용은 [부하 분산 장치에 대한 Azure Resource Manager 지원](load-balancer-arm.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="38460-119">For more information see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-cli-to-use-resource-manager"></a><span data-ttu-id="38460-120">Resource Manager를 사용하도록 CLI 설치</span><span class="sxs-lookup"><span data-stu-id="38460-120">Set up CLI to use Resource Manager</span></span>

1. <span data-ttu-id="38460-121">Azure CLI를 처음 사용하는 경우 [Azure CLI 설치 및 구성](../cli-install-nodejs.md) 을 참조하고 Azure 계정 및 구독을 선택하는 부분까지 관련 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="38460-121">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="38460-122">아래와 같이 **azure config mode** 명령을 실행하여 리소스 관리자 모드로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="38460-122">Run the **azure config mode** command to switch to Resource Manager mode, as shown below.</span></span>

    ```azurecli
        azure config mode arm
    ```

    <span data-ttu-id="38460-123">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="38460-123">Expected output:</span></span>

        info:    New mode is arm

## <a name="create-a-virtual-network-and-a-public-ip-address-for-the-front-end-ip-pool"></a><span data-ttu-id="38460-124">프런트 엔드 IP 풀에 대한 공용 IP 주소 및 가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="38460-124">Create a virtual network and a public IP address for the front-end IP pool</span></span>

1. <span data-ttu-id="38460-125">*NRPRG*라는 리소스 그룹을 사용하여 미국 동부 위치에 *NRPVnet*이라는 가상 네트워크(VNet)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="38460-125">Create a virtual network (VNet) named *NRPVnet* in the East US location using a resource group named *NRPRG*.</span></span>

    ```azurecli
        azure network vnet create NRPRG NRPVnet eastUS -a 10.0.0.0/16
    ```

    <span data-ttu-id="38460-126">*NRPVnet*에서 10.0.0.0/24의 CIDR 블록으로 *NRPVnetSubnet*이라는 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="38460-126">Create a subnet named *NRPVnetSubnet* with a CIDR block of 10.0.0.0/24 in *NRPVnet*.</span></span>

    ```azurecli
        azure network vnet subnet create NRPRG NRPVnet NRPVnetSubnet -a 10.0.0.0/24
    ```

2. <span data-ttu-id="38460-127">DNS 이름이 *loadbalancernrp.eastus.cloudapp.azure.com*인 프런트 엔드 IP 풀에서 사용할 *NRPPublicIP*라는 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="38460-127">Create a public IP address named *NRPPublicIP* to be used by a front-end IP pool with DNS name *loadbalancernrp.eastus.cloudapp.azure.com*.</span></span> <span data-ttu-id="38460-128">아래 명령은 정적 할당 형식 및 4분의 유휴 상태 시간 제한을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="38460-128">The command below uses the static allocation type and idle timeout of 4 minutes.</span></span>

    ```azurecli
        azure network public-ip create -g NRPRG -n NRPPublicIP -l eastus -d loadbalancernrp -a static -i 4
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="38460-129">부하 분산 장치는 FQDN으로 공용 IP의 도메인 레이블을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="38460-129">The load balancer will use the domain label of the public IP as its FQDN.</span></span> <span data-ttu-id="38460-130">이는 부하 분산 장치 FQDN(정규화된 도메인 이름)으로 클라우드 서비스를 사용하는 클래식 배포의 변경입니다.</span><span class="sxs-lookup"><span data-stu-id="38460-130">This a change from classic deployment, which uses the cloud service as the load balancer Fully Qualified Domain Name (FQDN).</span></span>
   > <span data-ttu-id="38460-131">이 예제에서는 FQDN이 *loadbalancernrp.eastus.cloudapp.azure.com*입니다.</span><span class="sxs-lookup"><span data-stu-id="38460-131">In this example, the FQDN is *loadbalancernrp.eastus.cloudapp.azure.com*.</span></span>

## <a name="create-a-load-balancer"></a><span data-ttu-id="38460-132">부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="38460-132">Create a load balancer</span></span>

<span data-ttu-id="38460-133">다음 명령은 *미국 동부* Azure 위치의 *NRPRG* 리소스 그룹에 *NRPlb*라는 부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="38460-133">The following command creates a load balancer named *NRPlb* in the *NRPRG* resource group in the *East US* Azure location.</span></span>

    ```azurecli
    azure network lb create NRPRG NRPlb eastus
    ```

## <a name="create-a-front-end-ip-pool-and-a-backend-address-pool"></a><span data-ttu-id="38460-134">프런트 엔드 IP 풀 및 백 엔드 주소 풀 만들기</span><span class="sxs-lookup"><span data-stu-id="38460-134">Create a front-end IP pool and a backend address pool</span></span>
<span data-ttu-id="38460-135">이 예제에서는 부하 분산 장치에 들어오는 네트워크 트래픽을 수신하는 프런트 엔드 IP 풀 및 프런트 엔드 풀이 부하 분산된 네트워크 트래픽을 보내는 백 엔드 IP 풀을 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="38460-135">This example demonstrates how to create the front-end IP pool that receives the incoming network traffic on the load balancer and the backend IP pool where the front-end pool sends the load balanced network traffic.</span></span>

1. <span data-ttu-id="38460-136">이전 단계에서 만든 공용 IP를 연결하는 프런트 엔드 IP 풀 및 부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="38460-136">Create a front-end IP pool associating the public IP created in the previous step and the load balancer.</span></span>

    ```azurecli
        azure network lb frontend-ip create nrpRG NRPlb NRPfrontendpool -i nrppublicip
    ```

2. <span data-ttu-id="38460-137">프런트 엔드 IP 풀에서 들어오는 트래픽을 받는 데 사용되는 백 엔드 주소 풀을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="38460-137">Set up a back-end address pool used to receive incoming traffic from the front-end IP pool.</span></span>

    ```azurecli
        azure network lb address-pool create NRPRG NRPlb NRPbackendpool
    ```

## <a name="create-lb-rules-nat-rules-and-probe"></a><span data-ttu-id="38460-138">LB 규칙, NAT 규칙 및 프로브 만들기</span><span class="sxs-lookup"><span data-stu-id="38460-138">Create LB rules, NAT rules, and probe</span></span>

<span data-ttu-id="38460-139">이 예제에서는 다음 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="38460-139">This example creates the following items.</span></span>

* <span data-ttu-id="38460-140">포트 21~포트 22에서 들어오는 모든 트래픽을 변환하는 NAT 규칙<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="38460-140">a NAT rule to translate all incoming traffic on port 21 to port 22<sup>1</sup></span></span>
* <span data-ttu-id="38460-141">포트 23~포트 22에서 들어오는 모든 트래픽을 변환하는 NAT 규칙</span><span class="sxs-lookup"><span data-stu-id="38460-141">a NAT rule to translate all incoming traffic on port 23 to port 22</span></span>
* <span data-ttu-id="38460-142">포트 80~포트 80에서 들어오는 모든 트래픽을 백 엔드 풀에 있는 주소로 분산하는 부하 분산 장치 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="38460-142">a load balancer rule to balance all incoming traffic on port 80 to port 80 on the addresses in the back-end pool.</span></span>
* <span data-ttu-id="38460-143">*HealthProbe.aspx*라는 페이지에 대한 상태를 확인할 프로브 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="38460-143">a probe rule to check the health status on a page named *HealthProbe.aspx*.</span></span>

<span data-ttu-id="38460-144"><sup>1</sup> NAT 규칙은 부하 분산 장치 뒤에 특정 가상 컴퓨터 인스턴스와 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38460-144"><sup>1</sup> NAT rules are associated to a specific virtual machine instance behind the load balancer.</span></span> <span data-ttu-id="38460-145">포트 21에 도착하는 네트워크 트래픽은 이 NAT 규칙과 연결된 포트 22의 특정 가상 컴퓨터에 보내집니다.</span><span class="sxs-lookup"><span data-stu-id="38460-145">The network traffic arriving on port 21 is sent to a specific virtual machine on port 22 associated with this NAT rule.</span></span> <span data-ttu-id="38460-146">NAT 규칙에 대한 프로토콜(UDP 또는 TCP)을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="38460-146">You must specify a protocol (UDP or TCP) for a NAT rule.</span></span> <span data-ttu-id="38460-147">두 프로토콜을 모두 동일한 포트에 할당할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="38460-147">Both protocols can't be assigned to the same port.</span></span>

1. <span data-ttu-id="38460-148">NAT 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="38460-148">Create the NAT rules.</span></span>

    ```azurecli
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh1 --protocol tcp --frontend-port 21 --backend-port 22
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh2 --protocol tcp --frontend-port 23 --backend-port 22
    ```

2. <span data-ttu-id="38460-149">부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="38460-149">Create a load balancer rule.</span></span>

    ```azurecli
        azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule --protocol tcp --frontend-port 80 --backend-port 80 --frontend-ip-name NRPfrontendpool --backend-address-pool-name NRPbackendpool
    ```

3. <span data-ttu-id="38460-150">상태 프로브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="38460-150">Create a health probe.</span></span>

    ```azurecli
        azure network lb probe create --resource-group nrprg --lb-name nrplb --name healthprobe --protocol "http" --port 80 --path healthprobe.aspx --interval 15 --count 4
    ```

4. <span data-ttu-id="38460-151">설정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="38460-151">Check your settings.</span></span>

    ```azurecli
        azure network lb show nrprg nrplb
    ```

    <span data-ttu-id="38460-152">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="38460-152">Expected output:</span></span>

        info:    Executing command network lb show
        + Looking up the load balancer "nrplb"
        + Looking up the public ip "NRPPublicIP"
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

## <a name="create-nics"></a><span data-ttu-id="38460-153">NIC 만들기</span><span class="sxs-lookup"><span data-stu-id="38460-153">Create NICs</span></span>

<span data-ttu-id="38460-154">NIC를 만들고(또는 기존 NIC 수정) NAT 규칙, 부하 분산 장치 규칙 및 프로브에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="38460-154">You need to create NICs (or modify existing ones) and associate them to NAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="38460-155">*lb-nic1-be*라는 NIC를 만들고 *rdp1* NAT 규칙 및 *NRPbackendpool* 백 엔드 주소 풀과 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="38460-155">Create a NIC named *lb-nic1-be*, and associate it with the *rdp1* NAT rule, and the *NRPbackendpool* back-end address pool.</span></span>

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" eastus
    ```

    <span data-ttu-id="38460-156">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="38460-156">Expected output:</span></span>

        info:    Executing command network nic create
        + Looking up the network interface "lb-nic1-be"
        + Looking up the subnet "nrpvnetsubnet"
        + Creating network interface "lb-nic1-be"
        + Looking up the network interface "lb-nic1-be"
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

2. <span data-ttu-id="38460-157">*lb-nic2-be*라는 NIC를 만들고 *rdp2* NAT 규칙 및 *NRPbackendpool* 백 엔드 주소 풀과 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="38460-157">Create a NIC named *lb-nic2-be*, and associate it with the *rdp2* NAT rule, and the *NRPbackendpool* back-end address pool.</span></span>

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" eastus
    ```

3. <span data-ttu-id="38460-158">*web1*이라는 VM(가상 컴퓨터)을 만들고 *lb-nic1-be*라는 NIC에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="38460-158">Create a virtual machine (VM) named *web1*, and associate it with the NIC named *lb-nic1-be*.</span></span> <span data-ttu-id="38460-159">*web1nrp* 라는 저장소 계정은 아래 명령을 실행하기 전에 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="38460-159">A storage account called *web1nrp* was created before running the command below.</span></span>

    ```azurecli
        azure vm create --resource-group nrprg --name web1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="38460-160">부하 분산 장치의 VM은 동일한 가용성 집합에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="38460-160">VMs in a load balancer need to be in the same availability set.</span></span> <span data-ttu-id="38460-161">`azure availset create` 을(를) 사용하여 가용성 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="38460-161">Use `azure availset create` to create an availability set.</span></span>

    <span data-ttu-id="38460-162">다음과 유사하게 출력되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="38460-162">The output should be similar to the following:</span></span>

        info:    Executing command vm create
        + Looking up the VM "web1"
        Enter username: azureuser
        Enter password for azureuser: *********
        Confirm password: *********
        info:    Using the VM Size "Standard_A1"
        info:    The [OS, Data] Disk or image configuration requires storage account
        + Looking up the storage account web1nrp
        + Looking up the availability set "nrp-avset"
        info:    Found an Availability set "nrp-avset"
        + Looking up the NIC "lb-nic1-be"
        info:    Found an existing NIC "lb-nic1-be"
        info:    Found an IP configuration with virtual network subnet id "/subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet" in the NIC "lb-nic1-be"
        info:    This is a NIC without publicIP configured
        + Creating VM "web1"
        info:    vm create command OK

    > [!NOTE]
    > <span data-ttu-id="38460-163">부하 분산 장치에 대해 만든 NIC가 부하 분산 장치 공용 IP 주소를 사용하여 인터넷에 연결되기 때문에 정보 메시지 **publicIP 구성 없는 NIC입니다** 가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="38460-163">The informational message **This is a NIC without publicIP configured** is expected since the NIC created for the load balancer connecting to Internet using the load balancer public IP address.</span></span>

    <span data-ttu-id="38460-164">*lb-nic1-be* NIC는 *rdp1* NAT 규칙에 연결되어 있으므로 부하 분산 장치의 포트 3441을 통해 RDP를 사용하여 *web1*에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38460-164">Since the *lb-nic1-be* NIC is associated with the *rdp1* NAT rule, you can connect to *web1* using RDP through port 3441 on the load balancer.</span></span>

4. <span data-ttu-id="38460-165">*web2*라는 VM(가상 컴퓨터)을 만들고 *lb-nic2-be*라는 NIC에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="38460-165">Create a virtual machine (VM) named *web2*, and associate it with the NIC named *lb-nic2-be*.</span></span> <span data-ttu-id="38460-166">*web1nrp* 라는 저장소 계정은 아래 명령을 실행하기 전에 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="38460-166">A storage account called *web1nrp* was created before running the command below.</span></span>

    ```azurecli
        azure vm create --resource-group nrprg --name web2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="38460-167">기존 부하 분산 장치 업데이트</span><span class="sxs-lookup"><span data-stu-id="38460-167">Update an existing load balancer</span></span>
<span data-ttu-id="38460-168">기존 부하 분산 장치를 참조하는 규칙을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38460-168">You can add rules referencing an existing load balancer.</span></span> <span data-ttu-id="38460-169">다음 예제에서는 새 부하 분산 장치 규칙은 기존 부하 분산 장치 **NRPlb**</span><span class="sxs-lookup"><span data-stu-id="38460-169">In the next example, a new load balancer rule is added to an existing load balancer **NRPlb**</span></span>

```azurecli
azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule2 --protocol tcp --frontend-port 8080 --backend-port 8051 --frontend-ip-name frontendnrppool --backend-address-pool-name NRPbackendpool
```

## <a name="delete-a-load-balancer"></a><span data-ttu-id="38460-170">부하 분산 장치 삭제</span><span class="sxs-lookup"><span data-stu-id="38460-170">Delete a load balancer</span></span>
<span data-ttu-id="38460-171">다음 명령을 사용하여 부하 분산 장치 제거:</span><span class="sxs-lookup"><span data-stu-id="38460-171">Use the following command to remove a load balancer:</span></span>

```azurecli
azure network lb delete --resource-group nrprg --name nrplb
```

## <a name="next-steps"></a><span data-ttu-id="38460-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="38460-172">Next steps</span></span>
[<span data-ttu-id="38460-173">내부 부하 분산 장치 구성 시작</span><span class="sxs-lookup"><span data-stu-id="38460-173">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-cli.md)

[<span data-ttu-id="38460-174">부하 분산 장치 배포 모드 구성</span><span class="sxs-lookup"><span data-stu-id="38460-174">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="38460-175">부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성</span><span class="sxs-lookup"><span data-stu-id="38460-175">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
