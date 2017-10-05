---
title: "Azure 내부 부하 분산 장치 만들기 - PowerShell 클래식 | Microsoft Docs"
description: "클래식 배포 모델에서 PowerShell을 사용하여 내부 부하 분산 장치를 만드는 방법에 대해 알아봅니다."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 3be93168-3787-45a5-a194-9124fe386493
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: f701fb3564c62cf8088cc4362a10c5e2c2301ae6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-powershell"></a><span data-ttu-id="b72dd-103">PowerShell을 사용하여 내부 부하 분산 장치(클래식) 만들기 시작</span><span class="sxs-lookup"><span data-stu-id="b72dd-103">Get started creating an internal load balancer (classic) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b72dd-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b72dd-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="b72dd-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b72dd-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="b72dd-106">Cloud services</span><span class="sxs-lookup"><span data-stu-id="b72dd-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="b72dd-107">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="b72dd-108">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-108">This article covers using the classic deployment model.</span></span> <span data-ttu-id="b72dd-109">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="b72dd-110">[Resource Manager 모델을 사용하여 이러한 단계를 수행하는](load-balancer-get-started-ilb-arm-ps.md) 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-110">Learn how to [perform these steps using the Resource Manager model](load-balancer-get-started-ilb-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-internal-load-balancer-set-for-virtual-machines"></a><span data-ttu-id="b72dd-111">가상 컴퓨터에 대한 내부 부하 분산 장치 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="b72dd-111">Create an internal load balancer set for virtual machines</span></span>

<span data-ttu-id="b72dd-112">내부 부하 분산 장치 집합과 이 집합으로 해당 트래픽을 전송할 서버를 만들려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-112">To create an internal load balancer set and the servers that will send their traffic to it, you have to do the following:</span></span>

1. <span data-ttu-id="b72dd-113">부하 분산 집합의 서버 간에 부하가 분산될 들어오는 트래픽의 끝점이 되는 내부 부하 분산의 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-113">Create an instance of Internal Load Balancing that will be the endpoint of incoming traffic to be load balanced across the servers of a load-balanced set.</span></span>
2. <span data-ttu-id="b72dd-114">들어오는 트래픽을 수신할 가상 컴퓨터에 해당하는 끝점을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-114">Add endpoints corresponding to the virtual machines that will be receiving the incoming traffic.</span></span>
3. <span data-ttu-id="b72dd-115">부하가 분산될 트래픽을 전송하는 서버가 해당 트래픽을 내부 부하 분산 인스턴스의 VIP(가상 IP) 주소로 전송하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-115">Configure the servers that will be sending the traffic to be load balanced to send their traffic to the virtual IP (VIP) address of the Internal Load Balancing instance.</span></span>

### <a name="step-1-create-an-internal-load-balancing-instance"></a><span data-ttu-id="b72dd-116">1단계: 내부 부하 분산 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="b72dd-116">Step 1: Create an Internal Load Balancing instance</span></span>

<span data-ttu-id="b72dd-117">기존 클라우드 서비스 또는 지역 가상 네트워크에 배포된 클라우드 서비스의 경우 다음 Windows PowerShell 명령을 사용하여 내부 부하 분산 인스턴스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-117">For an existing cloud service or a cloud service deployed under a regional virtual network, you can create an Internal Load Balancing instance with the following Windows PowerShell commands:</span></span>

```powershell
$svc="<Cloud Service Name>"
$ilb="<Name of your ILB instance>"
$subnet="<Name of the subnet within your virtual network>"
$IP="<The IPv4 address to use on the subnet-optional>"

Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP
```

<span data-ttu-id="b72dd-118">이 [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx) Windows PowerShell cmdlet 사용에서는 DefaultProbe 매개 변수 집합이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-118">Note that this use of the [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx) Windows PowerShell cmdlet uses the DefaultProbe parameter set.</span></span> <span data-ttu-id="b72dd-119">추가 매개 변수 집합에 대한 자세한 내용은 [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b72dd-119">For more information on additional parameter sets, see [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx).</span></span>

### <a name="step-2-add-endpoints-to-the-internal-load-balancing-instance"></a><span data-ttu-id="b72dd-120">2단계: 내부 부하 분산 인스턴스에 끝점 추가</span><span class="sxs-lookup"><span data-stu-id="b72dd-120">Step 2: Add endpoints to the Internal Load Balancing instance</span></span>

<span data-ttu-id="b72dd-121">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-121">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
$lbsetname="lbset"
$prot="tcp"
$locport=1433
$pubport=1433
$ilb="ilbset"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -Lbset $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM
```

### <a name="step-3-configure-your-servers-to-send-their-traffic-to-the-new-internal-load-balancing-endpoint"></a><span data-ttu-id="b72dd-122">3단계: 새 내부 부하 분산 끝점으로 트래픽을 전송하도록 서버 구성</span><span class="sxs-lookup"><span data-stu-id="b72dd-122">Step 3: Configure your servers to send their traffic to the new Internal Load Balancing endpoint</span></span>

<span data-ttu-id="b72dd-123">해당 트래픽의 부하가 분산될 서버에서 내부 부하 분산 인스턴스의 새 IP 주소(VIP)를 사용하도록 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-123">You have to  configure the servers whose traffic is going to be load balanced to use the new IP address (the VIP) of the Internal Load Balancing instance.</span></span> <span data-ttu-id="b72dd-124">이 주소는 내부 부하 분산 인스턴스가 수신 대기하는 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-124">This is the address on which the Internal Load Balancing instance is listening.</span></span> <span data-ttu-id="b72dd-125">대부분의 경우 내부 부하 분산 인스턴스의 VIP에 대한 DNS 레코드를 추가하거나 수정하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-125">In most cases, you need to just add or modify a DNS record for the VIP of the Internal Load Balancing instance.</span></span>

<span data-ttu-id="b72dd-126">내부 부하 분산 인스턴스를 만드는 동안 IP 주소를 지정한 경우 이미 VIP가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-126">If you specified the IP address during the creation of the Internal Load Balancing instance, you already have the VIP.</span></span> <span data-ttu-id="b72dd-127">그렇지 않으면 다음 명령을 통해 VIP를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-127">Otherwise, you can see the VIP from the following commands:</span></span>

```powershell
$svc="<Cloud Service Name>"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

<span data-ttu-id="b72dd-128">이러한 명령을 사용하려면 값을 입력하고 < 및 >를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-128">To use these commands, fill in the values and remove the < and >.</span></span> <span data-ttu-id="b72dd-129">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-129">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

<span data-ttu-id="b72dd-130">Get-AzureInternalLoadBalancer 명령 표시에서 IP 주소를 확인하고 필요한 경우 서버 또는 DNS 레코드를 변경하여 트래픽이 VIP로 전송되게 합니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-130">From the display of the Get-AzureInternalLoadBalancer command, note the IP address and make the necessary changes to your servers or DNS records to ensure that traffic gets sent to the VIP.</span></span>

> [!NOTE]
> <span data-ttu-id="b72dd-131">Microsoft Azure 플랫폼에서는 다양한 관리 시나리오에 공개적으로 라우팅할 수 있는 고정 IPv4 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-131">The Microsoft Azure platform uses a static, publicly routable IPv4 address for a variety of administrative scenarios.</span></span> <span data-ttu-id="b72dd-132">IP 주소는 168.63.129.16입니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-132">The IP address is 168.63.129.16.</span></span> <span data-ttu-id="b72dd-133">이 IP 주소를 방화벽으로 차단하면 안 됩니다. 예기치 않은 동작이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-133">This IP address should not be blocked by any firewalls, because it can cause unexpected behavior.</span></span>
> <span data-ttu-id="b72dd-134">Azure 내부 부하 분산과 관련하여 이 IP 주소는 부하 분산된 집합에서 가상 컴퓨터의 상태를 확인하기 위해 부하 분산 장치에서 프로브를 모니터링하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-134">With respect to Azure Internal Load Balancing, this IP address is used by monitoring probes from the load balancer to determine the health state for virtual machines in a load balanced set.</span></span> <span data-ttu-id="b72dd-135">내부적으로 부하 분산된 집합의 Azure 가상 컴퓨터로 트래픽을 제한하는 네트워크 보안 그룹이 사용된 경우 168.63.129.16의 트래픽을 허용하도록 네트워크 보안 규칙을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-135">If a Network Security Group is used to restrict traffic to Azure virtual machines in an internally load-balanced set or is applied to a Virtual Network Subnet, ensure that a Network Security Rule is added to allow traffic from 168.63.129.16.</span></span>

## <a name="example-of-internal-load-balancing"></a><span data-ttu-id="b72dd-136">내부 부하 분산의 예제</span><span class="sxs-lookup"><span data-stu-id="b72dd-136">Example of internal load balancing</span></span>

<span data-ttu-id="b72dd-137">두 예제 구성에 대한 부하 분산 집합을 만드는 완전한 프로세스의 단계별 지침은 다음 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b72dd-137">To step you through the end-to end process of creating a load-balanced set for two example configurations, see the following sections.</span></span>

### <a name="an-internet-facing-multi-tier-application"></a><span data-ttu-id="b72dd-138">인터넷 연결 다중 계층 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="b72dd-138">An Internet facing, multi-tier application</span></span>

<span data-ttu-id="b72dd-139">인터넷 연결 웹 서버 집합에 부하 분산 데이터베이스 서비스를 제공하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-139">You want to provide a load balanced database service for  a set of Internet-facing web servers.</span></span> <span data-ttu-id="b72dd-140">두 서버 집합은 단일 Azure 클라우드 서비스에서 호스트됩니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-140">Both sets of servers are hosted in a single Azure cloud service.</span></span> <span data-ttu-id="b72dd-141">TCP 포트 1433에 대한 웹 서버 트래픽을 데이터베이스 계층의 2개 가상 컴퓨터에 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-141">Web server traffic to TCP port 1433 must be distributed among two virtual machines in the database tier.</span></span> <span data-ttu-id="b72dd-142">그림 1은 구성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-142">Figure 1 shows the configuration.</span></span>

![데이터베이스 계층에 대한 내부 부하 분산 집합](./media/load-balancer-internal-getstarted/IC736321.png)

<span data-ttu-id="b72dd-144">구성은 다음과 같이 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-144">The configuration consists of the following:</span></span>

* <span data-ttu-id="b72dd-145">가상 컴퓨터를 호스트하는 기존 클라우드 서비스의 이름은 mytestcloud입니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-145">The existing cloud service hosting the virtual machines is named mytestcloud.</span></span>
* <span data-ttu-id="b72dd-146">두 기존 데이터베이스 서버 이름은 DB1, DB2입니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-146">The two existing database servers are named DB1, DB2.</span></span>
* <span data-ttu-id="b72dd-147">웹 계층의 웹 서버는 개인 IP 주소를 사용하여 데이터베이스 계층의 데이터베이스 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-147">Web servers in the web tier connect to the database servers in the database tier by using the private IP address.</span></span> <span data-ttu-id="b72dd-148">다른 옵션은 가상 네트워크에 자체 DNS를 사용하고 내부 부하 분산 장치 집합에 A 레코드를 수동으로 등록하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-148">Another option is to use your own DNS for the virtual network and manually register an A record for the internal load balancer set.</span></span>

<span data-ttu-id="b72dd-149">다음 명령은 **ILBset** 라는 새 내부 부하 분산 인스턴스를 구성하고 2개의 데이터베이스 서버에 해당하는 가상 컴퓨터에 끝점을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-149">The following commands configure a new Internal Load Balancing instance named **ILBset** and add endpoints to the virtual machines corresponding to the two database servers:</span></span>

```powershell
$svc="mytestcloud"
$ilb="ilbset"
Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb
$prot="tcp"
$locport=1433
$pubport=1433
$epname="TCP-1433-1433"
$lbsetname="lbset"
$vmname="DB1"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -LbSetName $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM

$epname="TCP-1433-1433-2"
$vmname="DB2"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -LbSetName $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM
```

## <a name="remove-an-internal-load-balancing-configuration"></a><span data-ttu-id="b72dd-150">내부 부하 분산 구성 제거</span><span class="sxs-lookup"><span data-stu-id="b72dd-150">Remove an Internal Load Balancing configuration</span></span>

<span data-ttu-id="b72dd-151">내부 부하 분산 장치 인스턴스에서 끝점인 가상 컴퓨터를 제거하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-151">To remove a virtual machine as an endpoint from an internal load balancer instance, use the following commands:</span></span>

```powershell
$svc="<Cloud service name>"
$vmname="<Name of the VM>"
$epname="<Name of the endpoint>"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

<span data-ttu-id="b72dd-152">이러한 명령을 사용하려면 값을 입력하고 < 및 >를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-152">To use these commands, fill in the values, removing the < and >.</span></span>

<span data-ttu-id="b72dd-153">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-153">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

<span data-ttu-id="b72dd-154">클라우드 서비스에서 내부 부하 분산 장치 인스턴스를 제거하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-154">To remove an internal load balancer instance from a cloud service, use the following commands:</span></span>

```powershell
$svc="<Cloud service name>"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

<span data-ttu-id="b72dd-155">이러한 명령을 사용하려면 값을 입력하고 < 및 >를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-155">To use these commands, fill in the value and remove the < and >.</span></span>

<span data-ttu-id="b72dd-156">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-156">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

## <a name="additional-information-about-internal-load-balancer-cmdlets"></a><span data-ttu-id="b72dd-157">내부 부하 분산 장치 cmdlet에 대한 추가 정보</span><span class="sxs-lookup"><span data-stu-id="b72dd-157">Additional information about internal load balancer cmdlets</span></span>

<span data-ttu-id="b72dd-158">내부 부하 분산 cmdlet에 대한 추가 정보를 얻으려면 Windows PowerShell 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b72dd-158">To obtain additional information about Internal Load Balancing cmdlets, run the following commands at a Windows PowerShell prompt:</span></span>

```powershell
Get-Help New-AzureInternalLoadBalancerConfig -full
Get-Help Add-AzureInternalLoadBalancer -full
Get-Help Get-AzureInternalLoadbalancer -full
Get-Help Remove-AzureInternalLoadBalancer -full
```

## <a name="next-steps"></a><span data-ttu-id="b72dd-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b72dd-159">Next steps</span></span>

[<span data-ttu-id="b72dd-160">원본 IP 선호도를 사용하여 부하 분산 장치 배포 모드 구성</span><span class="sxs-lookup"><span data-stu-id="b72dd-160">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="b72dd-161">부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성</span><span class="sxs-lookup"><span data-stu-id="b72dd-161">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

