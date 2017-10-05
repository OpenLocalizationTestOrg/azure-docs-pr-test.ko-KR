---
title: "PowerShell cmdlet을 사용하여 가상 컴퓨터 크기 집합 만들기 | Microsoft Docs"
description: "Azure PowerShell cmdlet을 사용하여 첫 번째 Azure 가상 컴퓨터 규모 집합 생성 및 관리 시작하기"
services: virtual-machines-windows
documentationcenter: 
author: danielsollondon
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 430d9d64-1f35-48f0-a4fd-9b69910ffa59
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/21/2017
ms.author: danielsollondon
ms.openlocfilehash: a3a36028a75d6cb7eb36277f3e2b5ab833c96a96
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="creating-virtual-machine-scale-sets-using-powershell-cmdlets"></a><span data-ttu-id="8ab5d-103">PowerShell cmdlet을 사용하여 가상 컴퓨터 크기 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="8ab5d-103">Creating Virtual Machine Scale Sets using PowerShell cmdlets</span></span>
<span data-ttu-id="8ab5d-104">이 문서에서는 VMSS(가상 컴퓨터 크기 집합)을 만드는 방법의 예제를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8ab5d-104">This article walks through an example of how to create a Virtual Machine scale set (VMSS).</span></span> <span data-ttu-id="8ab5d-105">관련 네트워킹 및 저장소를 포함한 세 개 노드의 크기 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8ab5d-105">It creates a scale set of three nodes, with associated Networking and Storage.</span></span>

## <a name="first-steps"></a><span data-ttu-id="8ab5d-106">첫 번째 단계</span><span class="sxs-lookup"><span data-stu-id="8ab5d-106">First Steps</span></span>
<span data-ttu-id="8ab5d-107">크기 집합을 만들고 유지 관리하는 데 필요한 PowerShell commandlet이 있는지 확인하려면 최신 Azure PowerShell 모듈이 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8ab5d-107">Ensure you have the latest Azure PowerShell module installed, to make sure you have the PowerShell commandlets needed to maintain, and create scale sets.</span></span>
<span data-ttu-id="8ab5d-108">사용 가능한 최신 Azure 모듈을 보려면 [여기](http://aka.ms/webpi-azps)에서 명령줄 도구로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="8ab5d-108">Go to the command line tools [here](http://aka.ms/webpi-azps) for the latest available Azure Modules.</span></span>

<span data-ttu-id="8ab5d-109">VMSS 관련 commandlet을 찾으려면 검색 문자열 \*VMSS\*를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="8ab5d-109">To find VMSS related commandlets, use the search string \*VMSS\*.</span></span> <span data-ttu-id="8ab5d-110">예: _gcm *vmss*_</span><span class="sxs-lookup"><span data-stu-id="8ab5d-110">For example, _gcm *vmss*_</span></span>

## <a name="creating-a-vmss"></a><span data-ttu-id="8ab5d-111">VMSS 만들기</span><span class="sxs-lookup"><span data-stu-id="8ab5d-111">Creating a VMSS</span></span>
#### <a name="create-resource-group"></a><span data-ttu-id="8ab5d-112">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="8ab5d-112">Create Resource Group</span></span>
```
$loc = 'westus';
$rgname = 'mynewrgwu';
  New-AzureRmResourceGroup -Name $rgname -Location $loc -Force;
```

### <a name="create-networking-vnet--subnet"></a><span data-ttu-id="8ab5d-113">네트워킹 만들기(VNET/서브넷)</span><span class="sxs-lookup"><span data-stu-id="8ab5d-113">Create Networking (VNET / Subnet)</span></span>
#### <a name="subnet-specification"></a><span data-ttu-id="8ab5d-114">서브넷 사양</span><span class="sxs-lookup"><span data-stu-id="8ab5d-114">Subnet Specification</span></span>
```
$subnetName = 'websubnet'
  $subnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix "10.0.0.0/24";
```

#### <a name="vnet-specification"></a><span data-ttu-id="8ab5d-115">VNET 사양</span><span class="sxs-lookup"><span data-stu-id="8ab5d-115">VNET Specification</span></span>
```
$vnet = New-AzureRmVirtualNetwork -Force -Name ('vnet' + $rgname) -ResourceGroupName $rgname -Location $loc -AddressPrefix "10.0.0.0/16" -Subnet $subnet;
$vnet = Get-AzureRmVirtualNetwork -Name ('vnet' + $rgname) -ResourceGroupName $rgname;

# In this case assume the new subnet is the only one
$subnetId = $vnet.Subnets[0].Id;
```

#### <a name="create-public-ip-resource-to-allow-external-access"></a><span data-ttu-id="8ab5d-116">외부 액세스를 허용하도록 공용 IP 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="8ab5d-116">Create Public IP Resource to Allow External Access</span></span>
<span data-ttu-id="8ab5d-117">이 항목은 부하 분산 장치에 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ab5d-117">This will be bound to the Load Balancer.</span></span>

```
$pubip = New-AzureRmPublicIpAddress -Force -Name ('pubip' + $rgname) -ResourceGroupName $rgname -Location $loc -AllocationMethod Dynamic -DomainNameLabel ('pubip' + $rgname);
$pubip = Get-AzureRmPublicIpAddress -Name ('pubip' + $rgname) -ResourceGroupName $rgname;
```

#### <a name="create-load-balancer"></a><span data-ttu-id="8ab5d-118">부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="8ab5d-118">Create Load Balancer</span></span>
```
$frontendName = 'fe' + $rgname
$backendAddressPoolName = 'bepool' + $rgname
$probeName = 'vmssprobe' + $rgname
$inboundNatPoolName = 'innatpool' + $rgname
$lbruleName = 'lbrule' + $rgname
$lbName = 'vmsslb' + $rgname

# Bind Public IP to Load Balancer
$frontend = New-AzureRmLoadBalancerFrontendIpConfig -Name $frontendName -PublicIpAddress $pubip
```

#### <a name="configure-load-balancer"></a><span data-ttu-id="8ab5d-119">부하 분산 장치 구성</span><span class="sxs-lookup"><span data-stu-id="8ab5d-119">Configure Load Balancer</span></span>
<span data-ttu-id="8ab5d-120">백 엔드 주소 풀 구성을 만들기는 크기 집합에 있는 VM의 NIC에서 공유됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ab5d-120">Create Backend Address Pool Config, this will be shared by the NICs of the VMs in the scale set.</span></span>

```
$backendAddressPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name $backendAddressPoolName
```

<span data-ttu-id="8ab5d-121">부하 분산된 프로브 포트를 설정하고 응용 프로그램에 적합하게 설정을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="8ab5d-121">Set Load Balanced Probe Port, change the settings as appropriate for your application.</span></span>

```
$probe = New-AzureRmLoadBalancerProbeConfig -Name $probeName -RequestPath healthcheck.aspx -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
```

<span data-ttu-id="8ab5d-122">부하 분산 장치를 통해 크기 집합의 VM에 직접 라우팅된 연결(부하 분산되지 않음)에 대한 인바운드 NAT 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8ab5d-122">Create an inbound NAT pool for direct routed connectivity (not load balanced) to the VMs in the scale set via the Load Balancer.</span></span> <span data-ttu-id="8ab5d-123">RDP를 사용하여 설명하는 것이고 응용 프로그램에 필요하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ab5d-123">This is to demonstrate using RDP and may not be required in your application.</span></span>

```
$frontendpoolrangestart = 3360
$frontendpoolrangeend = 3370
$backendvmport = 3389
$inboundNatPool = New-AzureRmLoadBalancerInboundNatPoolConfig -Name $inboundNatPoolName -FrontendIPConfigurationId `
$frontend.Id -Protocol Tcp -FrontendPortRangeStart $frontendpoolrangestart -FrontendPortRangeEnd $frontendpoolrangeend -BackendPort $backendvmport;
```

<span data-ttu-id="8ab5d-124">부하 분산 규칙을 만듭니다. 이 예제에서는 이전 단계의 설정을 사용한 부하 분산 포트 80 요청을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8ab5d-124">Create the Load Balanced Rule, this example shows load balancing port 80 requests, using the settings from previous steps.</span></span>

```
$protocol = 'Tcp'
$feLBPort = 80
$beLBPort = 80

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name $lbruleName `
-FrontendIPConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -Protocol $protocol -FrontendPort $feLBPort -BackendPort $beLBPort `
-IdleTimeoutInMinutes 15 -EnableFloatingIP -LoadDistribution SourceIP -Verbose;
```

<span data-ttu-id="8ab5d-125">구성을 사용하여 부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8ab5d-125">Create Load Balancer with configuration.</span></span>

```
$actualLb = New-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname -Location $loc `
-FrontendIpConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -LoadBalancingRule $lbrule -InboundNatPool $inboundNatPool -Verbose;
```

<span data-ttu-id="8ab5d-126">LB 설정을 확인하고 부하 분산 포트 구성을 확인합니다. 크기 집합의 VM을 만들 때까지 인바운드 NAT 규칙은 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8ab5d-126">Check  LB settings, check load balanced port configs, note, you will not see Inbound NAT rules until the VMs in the scale set are created.</span></span>

```
$expectedLb = Get-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname
```

##### <a name="configure-and-create-the-scale-set"></a><span data-ttu-id="8ab5d-127">크기 집합 구성 및 만들기</span><span class="sxs-lookup"><span data-stu-id="8ab5d-127">Configure and Create the scale set</span></span>
<span data-ttu-id="8ab5d-128">이 인프라 예제에서는 크기 집합에서 웹 트래픽 분산 및 확장을 설정하는 방법을 보여 주지만 여기에 지정된 VM 이미지에는 웹 서비스가 설치되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8ab5d-128">Note, this infrastructure example shows how to set up distribute and scale web traffic across the scale set, but the VMs Images specified here do not have any web services installed.</span></span>

```
# specify scale set Name
$vmssName = 'vmss' + $rgname;

## specify VMSS specific details
$adminUsername = 'azadmin';
$adminPassword = "Password1234!";

$PublisherName = 'MicrosoftWindowsServer'
$Offer         = 'WindowsServer'
$Sku          = '2012-R2-Datacenter'
$Version       = 'latest'
$vmNamePrefix = 'winvmss'

###add an extension
$extname = 'BGInfo';
$publisher = 'Microsoft.Compute';
$exttype = 'BGInfo';
$extver = '2.1';
```

<span data-ttu-id="8ab5d-129">부하 분산 장치 및 서브넷에 NIC 바인딩</span><span class="sxs-lookup"><span data-stu-id="8ab5d-129">Bind NIC to Load Balancer and Subnet</span></span>

```
$ipCfg = New-AzureRmVmssIPConfig -Name 'nic' `
-LoadBalancerInboundNatPoolsId $actualLb.InboundNatPools[0].Id `
-LoadBalancerBackendAddressPoolsId $actualLb.BackendAddressPools[0].Id `
-SubnetId $subnetId;
```

<span data-ttu-id="8ab5d-130">크기 집합 구성 만들기</span><span class="sxs-lookup"><span data-stu-id="8ab5d-130">Create scale set Config</span></span>

```
# Specify number of nodes
$numberofnodes = 3

$vmss = New-AzureRmVmssConfig -Location $loc -SkuCapacity $numberofnodes -SkuName 'Standard_A2' -UpgradePolicyMode 'automatic' `
    | Add-AzureRmVmssNetworkInterfaceConfiguration -Name $subnetName -Primary $true -IPConfiguration $ipCfg `
    | Set-AzureRmVmssOSProfile -ComputerNamePrefix $vmNamePrefix -AdminUsername $adminUsername -AdminPassword $adminPassword `
    | Set-AzureRmVmssStorageProfile -OsDiskCreateOption 'FromImage' -OsDiskCaching 'None' `
    -ImageReferenceOffer $Offer -ImageReferenceSku $Sku -ImageReferenceVersion $Version `
    -ImageReferencePublisher $PublisherName `
    | Add-AzureRmVmssExtension -Name $extname -Publisher $publisher -Type $exttype -TypeHandlerVersion $extver -AutoUpgradeMinorVersion $true
```

<span data-ttu-id="8ab5d-131">크기 집합 구성 빌드</span><span class="sxs-lookup"><span data-stu-id="8ab5d-131">Build scale set configuration</span></span>

```
New-AzureRmVmss -ResourceGroupName $rgname -Name $vmssName -VirtualMachineScaleSet $vmss -Verbose;
```

<span data-ttu-id="8ab5d-132">이제 크기 집합을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="8ab5d-132">Now you have created the scale set.</span></span> <span data-ttu-id="8ab5d-133">다음 예제에서 RDP를 사용하여 개별 VM에 대한 연결을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ab5d-133">You can test connecting to the individual VM using RDP in this example:</span></span>

```
VM0 : pubipmynewrgwu.westus.cloudapp.azure.com:3360
VM1 : pubipmynewrgwu.westus.cloudapp.azure.com:3361
VM2 : pubipmynewrgwu.westus.cloudapp.azure.com:3362
```
