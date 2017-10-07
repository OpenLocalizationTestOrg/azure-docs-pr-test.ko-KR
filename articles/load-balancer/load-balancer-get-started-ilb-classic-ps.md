---
title: "aaaCreate Azure 내부 부하 분산 장치-PowerShell 클래식 | Microsoft Docs"
description: "내부 프로그램 toocreate hello 클래식 배포 모델에서 PowerShell을 사용 하 여 분산 장치를 로드 하는 방법에 대해 알아봅니다"
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
ms.openlocfilehash: 382db80c42ffab09905513019b72e85a4f9dfeff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-powershell"></a><span data-ttu-id="a9f9a-103">PowerShell을 사용하여 내부 부하 분산 장치(클래식) 만들기 시작</span><span class="sxs-lookup"><span data-stu-id="a9f9a-103">Get started creating an internal load balancer (classic) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a9f9a-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9f9a-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="a9f9a-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a9f9a-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="a9f9a-106">Cloud services</span><span class="sxs-lookup"><span data-stu-id="a9f9a-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="a9f9a-107">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="a9f9a-108">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="a9f9a-109">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="a9f9a-110">너무 방법에 대해 알아봅니다[hello 리소스 관리자 모델을 사용 하 여 이러한 단계를 수행](load-balancer-get-started-ilb-arm-ps.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-110">Learn how too[perform these steps using hello Resource Manager model](load-balancer-get-started-ilb-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-internal-load-balancer-set-for-virtual-machines"></a><span data-ttu-id="a9f9a-111">가상 컴퓨터에 대한 내부 부하 분산 장치 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="a9f9a-111">Create an internal load balancer set for virtual machines</span></span>

<span data-ttu-id="a9f9a-112">내부 부하 분산 설정 하 고 해당 트래픽 tooit 보낼 서버 hello toocreate, toodo hello 다음을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-112">toocreate an internal load balancer set and hello servers that will send their traffic tooit, you have toodo hello following:</span></span>

1. <span data-ttu-id="a9f9a-113">내부 부하 분산의 부하 분산 된 집합의 hello 서버에 걸쳐 분산 된 들어오는 트래픽 toobe 부하의 hello 끝점 수 있는 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-113">Create an instance of Internal Load Balancing that will be hello endpoint of incoming traffic toobe load balanced across hello servers of a load-balanced set.</span></span>
2. <span data-ttu-id="a9f9a-114">Hello 들어오는 트래픽을 받게 되 toohello 가상 컴퓨터를 해당 끝점을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-114">Add endpoints corresponding toohello virtual machines that will be receiving hello incoming traffic.</span></span>
3. <span data-ttu-id="a9f9a-115">송신할 hello 트래픽 toobe 부하 분산 된 toosend 해당 트래픽을 toohello 가상 IP (VIP) 인스턴스의 주소 hello 내부 부하 분산 하는 hello 서버를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-115">Configure hello servers that will be sending hello traffic toobe load balanced toosend their traffic toohello virtual IP (VIP) address of hello Internal Load Balancing instance.</span></span>

### <a name="step-1-create-an-internal-load-balancing-instance"></a><span data-ttu-id="a9f9a-116">1단계: 내부 부하 분산 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="a9f9a-116">Step 1: Create an Internal Load Balancing instance</span></span>

<span data-ttu-id="a9f9a-117">기존 클라우드 서비스 또는 지역 가상 네트워크가 배포 된 클라우드 서비스에 대 한 다음 Windows PowerShell 명령을 hello로 내부 부하 분산 인스턴스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-117">For an existing cloud service or a cloud service deployed under a regional virtual network, you can create an Internal Load Balancing instance with hello following Windows PowerShell commands:</span></span>

```powershell
$svc="<Cloud Service Name>"
$ilb="<Name of your ILB instance>"
$subnet="<Name of hello subnet within your virtual network>"
$IP="<hello IPv4 address toouse on hello subnet-optional>"

Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP
```

<span data-ttu-id="a9f9a-118">hello의이 사용이 [Add-azureendpoint](https://msdn.microsoft.com/library/dn495300.aspx) hello DefaultProbe 매개 변수 집합을 사용 하 여 Windows PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-118">Note that this use of hello [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx) Windows PowerShell cmdlet uses hello DefaultProbe parameter set.</span></span> <span data-ttu-id="a9f9a-119">추가 매개 변수 집합에 대한 자세한 내용은 [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-119">For more information on additional parameter sets, see [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx).</span></span>

### <a name="step-2-add-endpoints-toohello-internal-load-balancing-instance"></a><span data-ttu-id="a9f9a-120">2 단계: 끝점 toohello 내부 부하 분산 인스턴스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-120">Step 2: Add endpoints toohello Internal Load Balancing instance</span></span>

<span data-ttu-id="a9f9a-121">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-121">Here is an example:</span></span>

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

### <a name="step-3-configure-your-servers-toosend-their-traffic-toohello-new-internal-load-balancing-endpoint"></a><span data-ttu-id="a9f9a-122">3 단계: 구성 서버 toosend 해당 트래픽을 toohello 새로운 내부 부하 분산 끝점</span><span class="sxs-lookup"><span data-stu-id="a9f9a-122">Step 3: Configure your servers toosend their traffic toohello new Internal Load Balancing endpoint</span></span>

<span data-ttu-id="a9f9a-123">진행 중인 toobe 부하 분산 된 toouse hello 새 IP 주소 (VIP hello) hello 인스턴스 내부 부하 분산의 트래픽은 hello 서버를 구성 너무 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-123">You have too configure hello servers whose traffic is going toobe load balanced toouse hello new IP address (hello VIP) of hello Internal Load Balancing instance.</span></span> <span data-ttu-id="a9f9a-124">내부 부하 분산 하는 hello 인스턴스가 수신 하는 hello 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-124">This is hello address on which hello Internal Load Balancing instance is listening.</span></span> <span data-ttu-id="a9f9a-125">Toojust 대부분의 경우에서 필요한 추가 하거나 hello 내부 부하 분산 인스턴스의 VIP hello에 대 한 DNS 레코드를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-125">In most cases, you need toojust add or modify a DNS record for hello VIP of hello Internal Load Balancing instance.</span></span>

<span data-ttu-id="a9f9a-126">Hello hello 내부 부하 분산 인스턴스를 만드는 동안 hello IP 주소를 지정한 경우 hello VIP이 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-126">If you specified hello IP address during hello creation of hello Internal Load Balancing instance, you already have hello VIP.</span></span> <span data-ttu-id="a9f9a-127">그렇지 않은 경우 명령 뒤 hello hello 프로덕션으로 VIP를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-127">Otherwise, you can see hello VIP from hello following commands:</span></span>

```powershell
$svc="<Cloud Service Name>"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

<span data-ttu-id="a9f9a-128">toouse hello 값 입력 제거 hello 이러한 명령은 < 및 >입니다.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-128">toouse these commands, fill in hello values and remove hello < and >.</span></span> <span data-ttu-id="a9f9a-129">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-129">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

<span data-ttu-id="a9f9a-130">Hello Get AzureInternalLoadBalancer 명령의 hello 디스플레이에서 hello IP 주소 기록한 hello 필요한 변경 tooyour 서버 또는 DNS 레코드 tooensure 트래픽 toohello VIP 전송 되 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-130">From hello display of hello Get-AzureInternalLoadBalancer command, note hello IP address and make hello necessary changes tooyour servers or DNS records tooensure that traffic gets sent toohello VIP.</span></span>

> [!NOTE]
> <span data-ttu-id="a9f9a-131">hello Microsoft Azure 플랫폼에는 다양 한 관리 시나리오에 대 한 정적, 공개적으로 라우팅 가능한 IPv4 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-131">hello Microsoft Azure platform uses a static, publicly routable IPv4 address for a variety of administrative scenarios.</span></span> <span data-ttu-id="a9f9a-132">hello IP 주소 168.63.129.16입니다.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-132">hello IP address is 168.63.129.16.</span></span> <span data-ttu-id="a9f9a-133">이 IP 주소를 방화벽으로 차단하면 안 됩니다. 예기치 않은 동작이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-133">This IP address should not be blocked by any firewalls, because it can cause unexpected behavior.</span></span>
> <span data-ttu-id="a9f9a-134">내부 부하 분산 측면 tooAzure와 hello 부하 분산 장치 toodetermine hello 상태에서 가상 컴퓨터 부하 분산 집합에 대해 프로브를 모니터링 하 여이 IP 주소 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-134">With respect tooAzure Internal Load Balancing, this IP address is used by monitoring probes from hello load balancer toodetermine hello health state for virtual machines in a load balanced set.</span></span> <span data-ttu-id="a9f9a-135">네트워크 보안 그룹 사용 되는 toorestrict 내부적으로 부하 분산 된 집합에 트래픽을 tooAzure 가상 컴퓨터는 되거나 적용 된 tooa 가상 네트워크 서브넷에 경우에 네트워크 보안 규칙 tooallow 트래픽을 168.63.129.16에서 추가 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-135">If a Network Security Group is used toorestrict traffic tooAzure virtual machines in an internally load-balanced set or is applied tooa Virtual Network Subnet, ensure that a Network Security Rule is added tooallow traffic from 168.63.129.16.</span></span>

## <a name="example-of-internal-load-balancing"></a><span data-ttu-id="a9f9a-136">내부 부하 분산의 예제</span><span class="sxs-lookup"><span data-stu-id="a9f9a-136">Example of internal load balancing</span></span>

<span data-ttu-id="a9f9a-137">toostep 2 가지의 구성 예제에 대 한 부하 분산 집합을 만드는 hello 끝 tooend 과정을 안내 합니다 참조 섹션에서는 다음 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-137">toostep you through hello end-tooend process of creating a load-balanced set for two example configurations, see hello following sections.</span></span>

### <a name="an-internet-facing-multi-tier-application"></a><span data-ttu-id="a9f9a-138">인터넷 연결 다중 계층 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="a9f9a-138">An Internet facing, multi-tier application</span></span>

<span data-ttu-id="a9f9a-139">Tooprovide 인터넷 연결 웹 서버 집합에 대 한 부하 분산 된 데이터베이스 서비스를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-139">You want tooprovide a load balanced database service for  a set of Internet-facing web servers.</span></span> <span data-ttu-id="a9f9a-140">두 서버 집합은 단일 Azure 클라우드 서비스에서 호스트됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-140">Both sets of servers are hosted in a single Azure cloud service.</span></span> <span data-ttu-id="a9f9a-141">웹 서버 트래픽을 tooTCP 포트 1433 hello 데이터베이스 계층의 가상 컴퓨터에 두 개의 배포 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-141">Web server traffic tooTCP port 1433 must be distributed among two virtual machines in hello database tier.</span></span> <span data-ttu-id="a9f9a-142">그림 1 hello 구성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-142">Figure 1 shows hello configuration.</span></span>

![Hello 데이터베이스 계층에 대 한 내부 부하 분산 된 집합](./media/load-balancer-internal-getstarted/IC736321.png)

<span data-ttu-id="a9f9a-144">hello 구성 hello 다음 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-144">hello configuration consists of hello following:</span></span>

* <span data-ttu-id="a9f9a-145">mytestcloud hello hello 가상 컴퓨터를 호스팅하는 기존 클라우드 서비스의 이름은입니다.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-145">hello existing cloud service hosting hello virtual machines is named mytestcloud.</span></span>
* <span data-ttu-id="a9f9a-146">hello 두 명의 기존 데이터베이스 서버 이름은 d b 2 d b 1입니다.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-146">hello two existing database servers are named DB1, DB2.</span></span>
* <span data-ttu-id="a9f9a-147">Hello 웹 계층의 웹 서버 hello 개인 IP 주소를 사용 하 여 hello 데이터베이스 계층의 toohello 데이터베이스 서버를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-147">Web servers in hello web tier connect toohello database servers in hello database tier by using hello private IP address.</span></span> <span data-ttu-id="a9f9a-148">또 다른 옵션은 toouse hello 가상 네트워크에 대 한 사용자 고유의 DNS 하 고 수동으로 hello 내부 부하 분산 장치 집합에 대 한 A 레코드를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-148">Another option is toouse your own DNS for hello virtual network and manually register an A record for hello internal load balancer set.</span></span>

<span data-ttu-id="a9f9a-149">hello 다음 명령을 새 인스턴스를 구성 내부 부하 분산 라는 **ILBset** toohello 두 데이터베이스 서버에 해당 하는 끝점 toohello 가상 컴퓨터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-149">hello following commands configure a new Internal Load Balancing instance named **ILBset** and add endpoints toohello virtual machines corresponding toohello two database servers:</span></span>

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

## <a name="remove-an-internal-load-balancing-configuration"></a><span data-ttu-id="a9f9a-150">내부 부하 분산 구성 제거</span><span class="sxs-lookup"><span data-stu-id="a9f9a-150">Remove an Internal Load Balancing configuration</span></span>

<span data-ttu-id="a9f9a-151">tooremove 인스턴스로부터 내부 부하 분산 장치, 다음 명령을 사용 하 여 hello 끝점으로 가상 컴퓨터:</span><span class="sxs-lookup"><span data-stu-id="a9f9a-151">tooremove a virtual machine as an endpoint from an internal load balancer instance, use hello following commands:</span></span>

```powershell
$svc="<Cloud service name>"
$vmname="<Name of hello VM>"
$epname="<Name of hello endpoint>"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

<span data-ttu-id="a9f9a-152">hello 값을 제거 하는 hello toouse 이러한 명령은 입력 < 및 >입니다.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-152">toouse these commands, fill in hello values, removing hello < and >.</span></span>

<span data-ttu-id="a9f9a-153">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-153">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

<span data-ttu-id="a9f9a-154">다음 명령을 사용 하 여 hello 클라우드 서비스에서 내부 부하 분산 장치 인스턴스 tooremove:</span><span class="sxs-lookup"><span data-stu-id="a9f9a-154">tooremove an internal load balancer instance from a cloud service, use hello following commands:</span></span>

```powershell
$svc="<Cloud service name>"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

<span data-ttu-id="a9f9a-155">이러한 명령의 toouse hello 값 입력 하 고 hello 제거 < 및 >입니다.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-155">toouse these commands, fill in hello value and remove hello < and >.</span></span>

<span data-ttu-id="a9f9a-156">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="a9f9a-156">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

## <a name="additional-information-about-internal-load-balancer-cmdlets"></a><span data-ttu-id="a9f9a-157">내부 부하 분산 장치 cmdlet에 대한 추가 정보</span><span class="sxs-lookup"><span data-stu-id="a9f9a-157">Additional information about internal load balancer cmdlets</span></span>

<span data-ttu-id="a9f9a-158">tooobtain hello 다음 Windows PowerShell 프롬프트에서 명령을 실행 합니다. 내부 부하 분산 cmdlet에 대 한 추가 정보:</span><span class="sxs-lookup"><span data-stu-id="a9f9a-158">tooobtain additional information about Internal Load Balancing cmdlets, run hello following commands at a Windows PowerShell prompt:</span></span>

```powershell
Get-Help New-AzureInternalLoadBalancerConfig -full
Get-Help Add-AzureInternalLoadBalancer -full
Get-Help Get-AzureInternalLoadbalancer -full
Get-Help Remove-AzureInternalLoadBalancer -full
```

## <a name="next-steps"></a><span data-ttu-id="a9f9a-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a9f9a-159">Next steps</span></span>

[<span data-ttu-id="a9f9a-160">원본 IP 선호도를 사용하여 부하 분산 장치 배포 모드 구성</span><span class="sxs-lookup"><span data-stu-id="a9f9a-160">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="a9f9a-161">부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성</span><span class="sxs-lookup"><span data-stu-id="a9f9a-161">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

