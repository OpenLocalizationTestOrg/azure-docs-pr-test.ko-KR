---
title: "IPv6를 사용하는 인터넷 연결 부하 분산 장치 만들기 - Azure CLI | Microsoft Docs"
description: "Azure CLI를 사용하여 Azure Resource Manager에서 IPv6으로 인터넷 연결 부하 분산 장치를 만드는 방법을 알아봅니다."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
keywords: "ipv6, Azure Load Balancer, 이중 스택, 공용 IP, 기본 ipv6, 모바일, iot"
ms.assetid: a1957c9c-9c1d-423e-9d5c-d71449bc1f37
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: efb4771800c42df544c3cc37d1d164045fdcaf3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-internet-facing-load-balancer-with-ipv6-in-azure-resource-manager-using-the-azure-cli"></a><span data-ttu-id="eb9f0-104">Azure CLI를 사용하여 Azure Resource Manager에서 IPv6으로 인터넷 연결 부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="eb9f0-104">Create an Internet facing load balancer with IPv6 in Azure Resource Manager using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="eb9f0-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="eb9f0-105">PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
> * [<span data-ttu-id="eb9f0-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="eb9f0-106">Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
> * [<span data-ttu-id="eb9f0-107">템플릿</span><span class="sxs-lookup"><span data-stu-id="eb9f0-107">Template</span></span>](load-balancer-ipv6-internet-template.md)

<span data-ttu-id="eb9f0-108">Azure 부하 분산 장치는 계층 4(TCP, UDP) 부하 분산 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-108">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="eb9f0-109">부하 분산 장치는 부하 분산 장치 집합에 있는 클라우드 서비스 또는 가상 컴퓨터의 정상 서비스 인스턴스 간에 들어오는 트래픽을 배포하여 고가용성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-109">The load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="eb9f0-110">Azure Load Balancer는 여러 포트, 여러 IP 주소 또는 둘 다에서 이러한 서비스를 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-110">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

## <a name="example-deployment-scenario"></a><span data-ttu-id="eb9f0-111">예제 배포 시나리오</span><span class="sxs-lookup"><span data-stu-id="eb9f0-111">Example deployment scenario</span></span>

<span data-ttu-id="eb9f0-112">다음 다이어그램은 이 문서에서 설명된 예제 템플릿을 사용하여 배포된 부하 분산 솔루션을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-112">The following diagram illustrates the load balancing solution being deployed using the example template described in this article.</span></span>

![부하 분산 장치 시나리오](./media/load-balancer-ipv6-internet-cli/lb-ipv6-scenario-cli.png)

<span data-ttu-id="eb9f0-114">이 시나리오에서는 다음과 같은 Azure 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-114">In this scenario you will create the following Azure resources:</span></span>

* <span data-ttu-id="eb9f0-115">2개의 가상 컴퓨터(VM)</span><span class="sxs-lookup"><span data-stu-id="eb9f0-115">two virtual machines (VMs)</span></span>
* <span data-ttu-id="eb9f0-116">할당된 IPv4 및 IPv6 주소를 사용하는 각 VM에 대한 가상 네트워크 인터페이스</span><span class="sxs-lookup"><span data-stu-id="eb9f0-116">a virtual network interface for each VM with both IPv4 and IPv6 addresses assigned</span></span>
* <span data-ttu-id="eb9f0-117">IPv4 및 IPv6 공용 IP 주소를 가진 인터넷 연결 부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="eb9f0-117">an Internet-facing Load Balancer with an IPv4 and an IPv6 Public IP address</span></span>
* <span data-ttu-id="eb9f0-118">두 개의 VM이 들어 있는 가용성 집합</span><span class="sxs-lookup"><span data-stu-id="eb9f0-118">an Availability Set to that contains the two VMs</span></span>
* <span data-ttu-id="eb9f0-119">공용 VIP를 개인 끝점으로 매핑하기 위한 두 개의 부하 분산 규칙</span><span class="sxs-lookup"><span data-stu-id="eb9f0-119">two load balancing rules to map the public VIPs to the private endpoints</span></span>

## <a name="deploying-the-solution-using-the-azure-cli"></a><span data-ttu-id="eb9f0-120">Azure CLI를 사용하여 솔루션 배포</span><span class="sxs-lookup"><span data-stu-id="eb9f0-120">Deploying the solution using the Azure CLI</span></span>

<span data-ttu-id="eb9f0-121">다음 단계에서는 CLI와 함께 Azure Resource Manager를 사용하여 인터넷 연결 부하 분산 장치를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-121">The following steps show how to create an Internet facing load balancer using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="eb9f0-122">Azure Resource Manager를 사용하면 각 리소스가 개별적으로 생성되고 구성된 다음, 함께 사용되어 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-122">With Azure Resource Manager, each resource is created and configured individually, and then put together to create a resource.</span></span>

<span data-ttu-id="eb9f0-123">부하 분산 장치를 배포하려면 다음 개체를 만들고 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-123">To deploy a load balancer, you create and configure the following objects:</span></span>

* <span data-ttu-id="eb9f0-124">프런트 엔드 IP 구성 - 들어오는 네트워크 트래픽에 대한 공용 IP 주소를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-124">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="eb9f0-125">백 엔드 주소 풀 - 부하 분산 장치의 네트워크 트래픽을 받는 가상 컴퓨터에 대한 NIC(네트워크 인터페이스)를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-125">Back-end address pool - contains network interfaces (NICs) for the virtual machines to receive network traffic from the load balancer.</span></span>
* <span data-ttu-id="eb9f0-126">부하 분산 규칙 - 백 엔드 주소 풀에 있는 포트에 부하 분산 장치의 공용 포트를 매핑하는 규칙을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-126">Load balancing rules - contains rules mapping a public port on the load balancer to port in the back-end address pool.</span></span>
* <span data-ttu-id="eb9f0-127">인바운드 NAT 규칙 - 백 엔드 주소 풀에 있는 특정 가상 컴퓨터에 대한 포트에 부하 분산 장치의 공용 포트를 매핑하는 규칙을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-127">Inbound NAT rules - contains rules mapping a public port on the load balancer to a port for a specific virtual machine in the back-end address pool.</span></span>
* <span data-ttu-id="eb9f0-128">프로브 - 백 엔드 주소 풀의 가상 컴퓨터 인스턴스의 가용성을 확인하는 데 사용하는 상태 프로브를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-128">Probes - contains health probes used to check availability of virtual machines instances in the back-end address pool.</span></span>

<span data-ttu-id="eb9f0-129">자세한 내용은 [부하 분산 장치에 대한 Azure Resource Manager 지원](load-balancer-arm.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-129">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-your-cli-environment-to-use-azure-resource-manager"></a><span data-ttu-id="eb9f0-130">Azure Resource Manager를 사용하도록 CLI 환경 설정</span><span class="sxs-lookup"><span data-stu-id="eb9f0-130">Set up your CLI environment to use Azure Resource Manager</span></span>

<span data-ttu-id="eb9f0-131">이 예제의 경우 PowerShell 명령 창에서 CLI 도구를 실행하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-131">For this example, we are running the CLI tools in a PowerShell command window.</span></span> <span data-ttu-id="eb9f0-132">Azure PowerShell cmdlet는 사용하지 않지만 가독성 및 재사용을 개선하기 위해 PowerShell의 스크립팅 기능은 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-132">We are not using the Azure PowerShell cmdlets but we use PowerShell's scripting capabilities to improve readability and reuse.</span></span>

1. <span data-ttu-id="eb9f0-133">Azure CLI를 처음 사용하는 경우 [Azure CLI 설치 및 구성](../cli-install-nodejs.md) 을 참조하고 Azure 계정 및 구독을 선택하는 부분까지 관련 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-133">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="eb9f0-134">**azure config mode** 명령을 실행하여 Resource Manager 모드로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-134">Run the **azure config mode** command to switch to Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="eb9f0-135">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="eb9f0-135">Expected output:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="eb9f0-136">Azure에 로그인하여 구독 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-136">Sign in to Azure and get a list of subscriptions.</span></span>

    ```azurecli
    azure login
    ```

    <span data-ttu-id="eb9f0-137">메시지가 표시되면 Azure 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-137">Enter your Azure credentials when prompted.</span></span>

    ```azurecli
    azure account list
    ```

    <span data-ttu-id="eb9f0-138">사용할 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-138">Pick the subscription you want to use.</span></span> <span data-ttu-id="eb9f0-139">다음 단계를 위해 구독 ID를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-139">Make note of the subscription Id for the next step.</span></span>

4. <span data-ttu-id="eb9f0-140">CLI 명령과 함께 사용하도록 PowerShell 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-140">Set up PowerShell variables for use with the CLI commands.</span></span>

    ```powershell
    $subscriptionid = "########-####-####-####-############"  # enter subscription id
    $location = "southcentralus"
    $rgName = "pscontosorg1southctrlus09152016"
    $vnetName = "contosoIPv4Vnet"
    $vnetPrefix = "10.0.0.0/16"
    $subnet1Name = "clicontosoIPv4Subnet1"
    $subnet1Prefix = "10.0.0.0/24"
    $subnet2Name = "clicontosoIPv4Subnet2"
    $subnet2Prefix = "10.0.1.0/24"
    $dnsLabel = "contoso09152016"
    $lbName = "myIPv4IPv6Lb"
    ```

## <a name="create-a-resource-group-a-load-balancer-a-virtual-network-and-subnets"></a><span data-ttu-id="eb9f0-141">리소스 그룹, 부하 분산 장치, 가상 네트워크 및 서브넷 만들기</span><span class="sxs-lookup"><span data-stu-id="eb9f0-141">Create a resource group, a load balancer, a virtual network, and subnets</span></span>

1. <span data-ttu-id="eb9f0-142">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="eb9f0-142">Create a resource group</span></span>

    ```azurecli
    azure group create $rgName $location
    ```

2. <span data-ttu-id="eb9f0-143">부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="eb9f0-143">Create a load balancer</span></span>

    ```azurecli
    $lb = azure network lb create --resource-group $rgname --location $location --name $lbName
    ```

3. <span data-ttu-id="eb9f0-144">VNet(가상 네트워크)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-144">Create a virtual network (VNet).</span></span>

    ```azurecli
    $vnet = azure network vnet create  --resource-group $rgname --name $vnetName --location $location --address-prefixes $vnetPrefix
    ```

    <span data-ttu-id="eb9f0-145">이 VNet에 두 개의 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-145">Create two subnets in this VNet.</span></span>

    ```azurecli
    $subnet1 = azure network vnet subnet create --resource-group $rgname --name $subnet1Name --address-prefix $subnet1Prefix --vnet-name $vnetName
    $subnet2 = azure network vnet subnet create --resource-group $rgname --name $subnet2Name --address-prefix $subnet2Prefix --vnet-name $vnetName
    ```

## <a name="create-public-ip-addresses-for-the-front-end-pool"></a><span data-ttu-id="eb9f0-146">프런트 엔드 풀에 대한 공용 IP 주소 만들기</span><span class="sxs-lookup"><span data-stu-id="eb9f0-146">Create public IP addresses for the front-end pool</span></span>

1. <span data-ttu-id="eb9f0-147">PowerShell 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-147">Set up the PowerShell variables</span></span>

    ```powershell
    $publicIpv4Name = "myIPv4Vip"
    $publicIpv6Name = "myIPv6Vip"
    ```

2. <span data-ttu-id="eb9f0-148">프론트 엔드 IP 풀에 대한 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-148">Create a public IP address the front-end IP pool.</span></span>

    ```azurecli
    $publicipV4 = azure network public-ip create --resource-group $rgname --name $publicIpv4Name --location $location --ip-version IPv4 --allocation-method Dynamic --domain-name-label $dnsLabel
    $publicipV6 = azure network public-ip create --resource-group $rgname --name $publicIpv6Name --location $location --ip-version IPv6 --allocation-method Dynamic --domain-name-label $dnsLabel
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="eb9f0-149">부하 분산 장치는 공용 IP의 도메인 레이블을 FQDN으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-149">The load balancer uses the domain label of the public IP as its FQDN.</span></span> <span data-ttu-id="eb9f0-150">이는 클래식 배포의 변경으로, 클라우드 서비스 이름을 부하 분산 장치 FQDN으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-150">This a change from classic deployment, which uses the cloud service name as the load balancer FQDN.</span></span>
    > <span data-ttu-id="eb9f0-151">이 예제에서 FQDN은 *contoso09152016.southcentralus.cloudapp.azure.com*입니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-151">In this example, the FQDN is *contoso09152016.southcentralus.cloudapp.azure.com*.</span></span>

## <a name="create-front-end-and-back-end-pools"></a><span data-ttu-id="eb9f0-152">프런트 엔드 및 백 엔드 풀 만들기</span><span class="sxs-lookup"><span data-stu-id="eb9f0-152">Create front-end and back-end pools</span></span>

<span data-ttu-id="eb9f0-153">이 예제에서는 부하 분산 장치에 들어오는 네트워크 트래픽을 수신하는 프런트 엔드 IP 풀 및 프런트 엔드 풀이 부하 분산된 네트워크 트래픽을 보내는 백 엔드 IP 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-153">This example creates the front-end IP pool that receives the incoming network traffic on the load balancer and the back-end IP pool where the front-end pool sends the load balanced network traffic.</span></span>

1. <span data-ttu-id="eb9f0-154">PowerShell 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-154">Set up the PowerShell variables</span></span>

    ```powershell
    $frontendV4Name = "FrontendVipIPv4"
    $frontendV6Name = "FrontendVipIPv6"
    $backendAddressPoolV4Name = "BackendPoolIPv4"
    $backendAddressPoolV6Name = "BackendPoolIPv6"
    ```

2. <span data-ttu-id="eb9f0-155">이전 단계에서 만든 공용 IP를 연결하는 프런트 엔드 IP 풀 및 부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-155">Create a front-end IP pool associating the public IP created in the previous step and the load balancer.</span></span>

    ```azurecli
    $frontendV4 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV4Name --public-ip-name $publicIpv4Name --lb-name $lbName
    $frontendV6 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV6Name --public-ip-name $publicIpv6Name --lb-name $lbName
    $backendAddressPoolV4 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV4Name --lb-name $lbName
    $backendAddressPoolV6 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV6Name --lb-name $lbName
    ```

## <a name="create-the-probe-nat-rules-and-lb-rules"></a><span data-ttu-id="eb9f0-156">LB 규칙, NAT 규칙 및 프로브 만들기</span><span class="sxs-lookup"><span data-stu-id="eb9f0-156">Create the probe, NAT rules, and LB rules</span></span>

<span data-ttu-id="eb9f0-157">이 예제에서는 다음 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-157">This example creates the following items:</span></span>

* <span data-ttu-id="eb9f0-158">TCP 포트 80에 대한 연결을 확인하기 위한 프로브 규칙</span><span class="sxs-lookup"><span data-stu-id="eb9f0-158">a probe rule to check for connectivity to TCP port 80</span></span>
* <span data-ttu-id="eb9f0-159">포트 3389에 들어오는 모든 트래픽을 RDP<sup>1</sup>에 대한 포트 3389로 변환하는 NAT 규칙</span><span class="sxs-lookup"><span data-stu-id="eb9f0-159">a NAT rule to translate all incoming traffic on port 3389 to port 3389 for RDP<sup>1</sup></span></span>
* <span data-ttu-id="eb9f0-160">포트 3391에 들어오는 모든 트래픽을 RDP<sup>1</sup>에 대한 포트 3389로 변환하는 NAT 규칙</span><span class="sxs-lookup"><span data-stu-id="eb9f0-160">a NAT rule to translate all incoming traffic on port 3391 to port 3389 for RDP<sup>1</sup></span></span>
* <span data-ttu-id="eb9f0-161">포트 80~포트 80에서 들어오는 모든 트래픽을 백 엔드 풀에 있는 주소로 분산하는 부하 분산 장치 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-161">a load balancer rule to balance all incoming traffic on port 80 to port 80 on the addresses in the back-end pool.</span></span>

<span data-ttu-id="eb9f0-162"><sup>1</sup> NAT 규칙은 부하 분산 장치 뒤에 특정 가상 컴퓨터 인스턴스와 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-162"><sup>1</sup> NAT rules are associated to a specific virtual machine instance behind the load balancer.</span></span> <span data-ttu-id="eb9f0-163">포트 3389에 도착하는 네트워크 트래픽은 이 NAT 규칙과 연결된 포트의 특정 가상 컴퓨터에 보내집니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-163">The network traffic arriving on port 3389 is sent to the specific virtual machine and port associated with the NAT rule.</span></span> <span data-ttu-id="eb9f0-164">NAT 규칙에 대한 프로토콜(UDP 또는 TCP)을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-164">You must specify a protocol (UDP or TCP) for a NAT rule.</span></span> <span data-ttu-id="eb9f0-165">두 프로토콜을 모두 동일한 포트에 할당할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-165">Both protocols can't be assigned to the same port.</span></span>

1. <span data-ttu-id="eb9f0-166">PowerShell 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-166">Set up the PowerShell variables</span></span>

    ```powershell
    $probeV4V6Name = "ProbeForIPv4AndIPv6"
    $natRule1V4Name = "NatRule-For-Rdp-VM1"
    $natRule2V4Name = "NatRule-For-Rdp-VM2"
    $lbRule1V4Name = "LBRuleForIPv4-Port80"
    $lbRule1V6Name = "LBRuleForIPv6-Port80"
    ```

2. <span data-ttu-id="eb9f0-167">프로브 만들기</span><span class="sxs-lookup"><span data-stu-id="eb9f0-167">Create the probe</span></span>

    <span data-ttu-id="eb9f0-168">다음 예제는 15초마다 백 엔드 TCP 포트 80에 대한 연결을 확인하는 TCP 프로브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-168">The following example creates a TCP probe that checks for connectivity to back-end TCP port 80 every 15 seconds.</span></span> <span data-ttu-id="eb9f0-169">두 차례의 연속 실패 후에는 사용할 수 없는 백 엔드 리소스를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-169">It will mark the back-end resource unavailable after two consecutive failures.</span></span>

    ```azurecli
    $probeV4V6 = azure network lb probe create --resource-group $rgname --name $probeV4V6Name --protocol tcp --port 80 --interval 15 --count 2 --lb-name $lbName
    ```

3. <span data-ttu-id="eb9f0-170">백 엔드 리소스에 대한 RDP 연결을 허용하는 인바운드 NAT 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="eb9f0-170">Create inbound NAT rules that allow RDP connections to the back-end resources</span></span>

    ```azurecli
    $inboundNatRuleRdp1 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule1V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3389 --backend-port 3389 --lb-name $lbName
    $inboundNatRuleRdp2 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule2V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3391 --backend-port 3389 --lb-name $lbName
    ```

4. <span data-ttu-id="eb9f0-171">어떤 프런트 엔드가 요청을 수신하는지에 따라 다른 백 엔드 포트로 트래픽을 전송 하는 부하 분산 장치 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-171">Create a load balancer rules that send traffic to different back-end ports depending on which front end received the request</span></span>

    ```azurecli
    $lbruleIPv4 = azure network lb rule create --resource-group $rgname --name $lbRule1V4Name --frontend-ip-name $frontendV4Name --backend-address-pool-name $backendAddressPoolV4Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 80 --lb-name $lbName
    $lbruleIPv6 = azure network lb rule create --resource-group $rgname --name $lbRule1V6Name --frontend-ip-name $frontendV6Name --backend-address-pool-name $backendAddressPoolV6Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 8080 --lb-name $lbName
    ```

5. <span data-ttu-id="eb9f0-172">설정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-172">Check your settings</span></span>

    ```azurecli
    azure network lb show --resource-group $rgName --name $lbName
    ```

    <span data-ttu-id="eb9f0-173">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="eb9f0-173">Expected output:</span></span>

        info:    Executing command network lb show
        info:    Looking up the load balancer "myIPv4IPv6Lb"
        data:    Id                              : /subscriptions/########-####-####-####-############/resourceGroups/pscontosorg1southctrlus09152016/providers/Microsoft.Network/loadBalancers/myIPv4IPv6Lb
        data:    Name                            : myIPv4IPv6Lb
        data:    Type                            : Microsoft.Network/loadBalancers
        data:    Location                        : southcentralus
        data:    Provisioning state              : Succeeded
        data:
        data:    Frontend IP configurations:
        data:    Name             Provisioning state  Private IP allocation  Private IP   Subnet  Public IP
        data:    ---------------  ------------------  ---------------------  -----------  ------  ---------
        data:    FrontendVipIPv4  Succeeded           Dynamic                                     myIPv4Vip
        data:    FrontendVipIPv6  Succeeded           Dynamic                                     myIPv6Vip
        data:
        data:    Probes:
        data:    Name                 Provisioning state  Protocol  Port  Path  Interval  Count
        data:    -------------------  ------------------  --------  ----  ----  --------  -----
        data:    ProbeForIPv4AndIPv6  Succeeded           Tcp       80          15        2
        data:
        data:    Backend Address Pools:
        data:    Name             Provisioning state
        data:    ---------------  ------------------
        data:    BackendPoolIPv4  Succeeded
        data:    BackendPoolIPv6  Succeeded
        data:
        data:    Load Balancing Rules:
        data:    Name                  Provisioning state  Load distribution  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    --------------------  ------------------  -----------------  --------  -------------  ------------  ------------------  -----------------------
        data:    LBRuleForIPv4-Port80  Succeeded           Default            Tcp       80             80            false               4
        data:    LBRuleForIPv6-Port80  Succeeded           Default            Tcp       80             8080          false               4
        data:
        data:    Inbound NAT Rules:
        data:    Name                 Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    -------------------  ------------------  --------  -------------  ------------  ------------------  -----------------------
        data:    NatRule-For-Rdp-VM1  Succeeded           Tcp       3389           3389          false               4
        data:    NatRule-For-Rdp-VM2  Succeeded           Tcp       3391           3389          false               4
        info:    network lb show

## <a name="create-nics"></a><span data-ttu-id="eb9f0-174">NIC 만들기</span><span class="sxs-lookup"><span data-stu-id="eb9f0-174">Create NICs</span></span>

<span data-ttu-id="eb9f0-175">NIC를 만들어 NAT 규칙, 부하 분산 장치 규칙 및 프로브에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-175">Create NICs and associate them to NAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="eb9f0-176">PowerShell 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-176">Set up the PowerShell variables</span></span>

    ```powershell
    $nic1Name = "myIPv4IPv6Nic1"
    $nic2Name = "myIPv4IPv6Nic2"
    $subnet1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet1Name"
    $subnet2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet2Name"
    $backendAddressPoolV4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV4Name"
    $backendAddressPoolV6Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV6Name"
    $natRule1V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule1V4Name"
    $natRule2V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule2V4Name"
    ```

2. <span data-ttu-id="eb9f0-177">각 백 엔드에 대한 NIC를 만들고 IPv6 구성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-177">Create a NIC for each back-end and add an IPv6 configuration.</span></span>

    ```azurecli
    $nic1 = azure network nic create --name $nic1Name --resource-group $rgname --location $location --private-ip-version "IPv4" --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule1V4Id
    $nic1IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic1Name

    $nic2 = azure network nic create --name $nic2Name --resource-group $rgname --location $location --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule2V4Id
    $nic2IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic2Name
    ```

## <a name="create-the-back-end-vm-resources-and-attach-each-nic"></a><span data-ttu-id="eb9f0-178">백 엔드 VM 리소스를 만들고 각 NIC를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-178">Create the back-end VM resources and attach each NIC</span></span>

<span data-ttu-id="eb9f0-179">VM을 만들려면 저장소 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-179">To create VMs, you must have a storage account.</span></span> <span data-ttu-id="eb9f0-180">부하 분산을 하려면 VM이 가용성 집합의 구성원이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-180">For load balancing, the VMs need to be members of an availability set.</span></span> <span data-ttu-id="eb9f0-181">VM 만들기에 대한 자세한 내용은 [PowerShell을 사용하여 Azure VM 만들기](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="eb9f0-181">For more information about creating VMs, see [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span></span>

1. <span data-ttu-id="eb9f0-182">PowerShell 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-182">Set up the PowerShell variables</span></span>

    ```powershell
    $storageAccountName = "ps08092016v6sa0"
    $availabilitySetName = "myIPv4IPv6AvailabilitySet"
    $vm1Name = "myIPv4IPv6VM1"
    $vm2Name = "myIPv4IPv6VM2"
    $nic1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic1Name"
    $nic2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic2Name"
    $disk1Name = "WindowsVMosDisk1"
    $disk2Name = "WindowsVMosDisk2"
    $osDisk1Uri = "https://$storageAccountName.blob.core.windows.net/vhds/$disk1Name.vhd"
    $osDisk2Uri = "https://$storageAccountName.blob.core.windows.net/vhds/$disk2Name.vhd"
    $imageurn "MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest"
    $vmUserName = "vmUser"
    $mySecurePassword = "PlainTextPassword*1"
    ```

    > [!WARNING]
    > <span data-ttu-id="eb9f0-183">이 예제에서는 일반 텍스트로 VM에 대한 사용자 이름 및 비밀번호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-183">This example uses the username and password for the VMs in clear text.</span></span> <span data-ttu-id="eb9f0-184">일반 텍스트로 자격 증명을 사용하는 경우 적절한 주의를 기울여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-184">Appropriate care must be taken when using credentials in the clear.</span></span> <span data-ttu-id="eb9f0-185">PowerShell에서 자격 증명을 처리하는 보다 안전한 방법은 [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-185">For a more secure method of handling credentials in PowerShell, see the [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

2. <span data-ttu-id="eb9f0-186">저장소 계정 및 가용성 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="eb9f0-186">Create the storage account and availability set</span></span>

    <span data-ttu-id="eb9f0-187">VM을 만들 때 기존 저장소 계정을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-187">You may use an existing storage account when you create the VMs.</span></span> <span data-ttu-id="eb9f0-188">다음 명령을 사용해 새로운 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-188">The following command creates a new storage account.</span></span>

    ```azurecli
    $storageAcc = azure storage account create $storageAccountName --resource-group $rgName --location $location --sku-name "LRS" --kind "Storage"
    ```

    <span data-ttu-id="eb9f0-189">다음으로 가용성 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eb9f0-189">Next, create the availability set.</span></span>

    ```azurecli
    $availabilitySet = azure availset create --name $availabilitySetName --resource-group $rgName --location $location
    ```

3. <span data-ttu-id="eb9f0-190">연결된 NIC로 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="eb9f0-190">Create the virtual machines with the associated NICs</span></span>

    ```azurecli
    $vm1 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm1Name --nic-id $nic1Id --os-disk-vhd $osDisk1Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension

    $vm2 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm2Name --nic-id $nic2Id --os-disk-vhd $osDisk2Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension
    ```

## <a name="next-steps"></a><span data-ttu-id="eb9f0-191">다음 단계</span><span class="sxs-lookup"><span data-stu-id="eb9f0-191">Next steps</span></span>

[<span data-ttu-id="eb9f0-192">내부 부하 분산 장치 구성 시작</span><span class="sxs-lookup"><span data-stu-id="eb9f0-192">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-cli.md)

[<span data-ttu-id="eb9f0-193">부하 분산 장치 배포 모드 구성</span><span class="sxs-lookup"><span data-stu-id="eb9f0-193">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="eb9f0-194">부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성</span><span class="sxs-lookup"><span data-stu-id="eb9f0-194">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
