---
title: "PowerShell cmdlet을 사용 하 여 설정 하는 가상 컴퓨터 크기 aaaCreating | Microsoft Docs"
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
ms.openlocfilehash: 7979be367d04c904b60d78849c1b751a52cc8caf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-virtual-machine-scale-sets-using-powershell-cmdlets"></a><span data-ttu-id="596b5-103">PowerShell cmdlet을 사용하여 가상 컴퓨터 크기 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="596b5-103">Creating Virtual Machine Scale Sets using PowerShell cmdlets</span></span>
<span data-ttu-id="596b5-104">이 문서는 어떻게 toocreate는 가상 컴퓨터 크기 집합 (VMSS)의 예를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="596b5-104">This article walks through an example of how toocreate a Virtual Machine scale set (VMSS).</span></span> <span data-ttu-id="596b5-105">관련 네트워킹 및 저장소를 포함한 세 개 노드의 크기 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="596b5-105">It creates a scale set of three nodes, with associated Networking and Storage.</span></span>

## <a name="first-steps"></a><span data-ttu-id="596b5-106">첫 번째 단계</span><span class="sxs-lookup"><span data-stu-id="596b5-106">First Steps</span></span>
<span data-ttu-id="596b5-107">Hello 최신 Azure PowerShell 모듈이 설치 되어 있는, toomake hello PowerShell commandlet 있는지 toomaintain, 필요한 및 크기 집합 만들기를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="596b5-107">Ensure you have hello latest Azure PowerShell module installed, toomake sure you have hello PowerShell commandlets needed toomaintain, and create scale sets.</span></span>
<span data-ttu-id="596b5-108">Toohello 명령줄 도구를 이동 [여기](http://aka.ms/webpi-azps) hello 최신 사용 가능한 Azure 모듈에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="596b5-108">Go toohello command line tools [here](http://aka.ms/webpi-azps) for hello latest available Azure Modules.</span></span>

<span data-ttu-id="596b5-109">VMSS toofind 관련 commandlet를 hello 검색 문자열을 사용 하 여 \*VMSS\*합니다.</span><span class="sxs-lookup"><span data-stu-id="596b5-109">toofind VMSS related commandlets, use hello search string \*VMSS\*.</span></span> <span data-ttu-id="596b5-110">예: _gcm *vmss*_</span><span class="sxs-lookup"><span data-stu-id="596b5-110">For example, _gcm *vmss*_</span></span>

## <a name="creating-a-vmss"></a><span data-ttu-id="596b5-111">VMSS 만들기</span><span class="sxs-lookup"><span data-stu-id="596b5-111">Creating a VMSS</span></span>
#### <a name="create-resource-group"></a><span data-ttu-id="596b5-112">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="596b5-112">Create Resource Group</span></span>
```
$loc = 'westus';
$rgname = 'mynewrgwu';
  New-AzureRmResourceGroup -Name $rgname -Location $loc -Force;
```

### <a name="create-networking-vnet--subnet"></a><span data-ttu-id="596b5-113">네트워킹 만들기(VNET/서브넷)</span><span class="sxs-lookup"><span data-stu-id="596b5-113">Create Networking (VNET / Subnet)</span></span>
#### <a name="subnet-specification"></a><span data-ttu-id="596b5-114">서브넷 사양</span><span class="sxs-lookup"><span data-stu-id="596b5-114">Subnet Specification</span></span>
```
$subnetName = 'websubnet'
  $subnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix "10.0.0.0/24";
```

#### <a name="vnet-specification"></a><span data-ttu-id="596b5-115">VNET 사양</span><span class="sxs-lookup"><span data-stu-id="596b5-115">VNET Specification</span></span>
```
$vnet = New-AzureRmVirtualNetwork -Force -Name ('vnet' + $rgname) -ResourceGroupName $rgname -Location $loc -AddressPrefix "10.0.0.0/16" -Subnet $subnet;
$vnet = Get-AzureRmVirtualNetwork -Name ('vnet' + $rgname) -ResourceGroupName $rgname;

# In this case assume hello new subnet is hello only one
$subnetId = $vnet.Subnets[0].Id;
```

#### <a name="create-public-ip-resource-tooallow-external-access"></a><span data-ttu-id="596b5-116">공용 IP 리소스 tooAllow 외부 액세스 만들기</span><span class="sxs-lookup"><span data-stu-id="596b5-116">Create Public IP Resource tooAllow External Access</span></span>
<span data-ttu-id="596b5-117">바인딩된 toohello 부하 분산 장치 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="596b5-117">This will be bound toohello Load Balancer.</span></span>

```
$pubip = New-AzureRmPublicIpAddress -Force -Name ('pubip' + $rgname) -ResourceGroupName $rgname -Location $loc -AllocationMethod Dynamic -DomainNameLabel ('pubip' + $rgname);
$pubip = Get-AzureRmPublicIpAddress -Name ('pubip' + $rgname) -ResourceGroupName $rgname;
```

#### <a name="create-load-balancer"></a><span data-ttu-id="596b5-118">부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="596b5-118">Create Load Balancer</span></span>
```
$frontendName = 'fe' + $rgname
$backendAddressPoolName = 'bepool' + $rgname
$probeName = 'vmssprobe' + $rgname
$inboundNatPoolName = 'innatpool' + $rgname
$lbruleName = 'lbrule' + $rgname
$lbName = 'vmsslb' + $rgname

# Bind Public IP tooLoad Balancer
$frontend = New-AzureRmLoadBalancerFrontendIpConfig -Name $frontendName -PublicIpAddress $pubip
```

#### <a name="configure-load-balancer"></a><span data-ttu-id="596b5-119">부하 분산 장치 구성</span><span class="sxs-lookup"><span data-stu-id="596b5-119">Configure Load Balancer</span></span>
<span data-ttu-id="596b5-120">Hello 크기 집합의 hello Vm의 hello Nic에서 공유할 수는이, 백 엔드 주소 풀 Config를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="596b5-120">Create Backend Address Pool Config, this will be shared by hello NICs of hello VMs in hello scale set.</span></span>

```
$backendAddressPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name $backendAddressPoolName
```

<span data-ttu-id="596b5-121">부하 분산 된 프로브 포트 설정, 응용 프로그램에 맞게 hello 설정을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="596b5-121">Set Load Balanced Probe Port, change hello settings as appropriate for your application.</span></span>

```
$probe = New-AzureRmLoadBalancerProbeConfig -Name $probeName -RequestPath healthcheck.aspx -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
```

<span data-ttu-id="596b5-122">직접 라우팅된 연결 (하지 부하 분산)에 대 한 인바운드 NAT 풀 만들기 hello 부하 분산 장치를 통해 Vm toohello hello 규모에 맞게 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="596b5-122">Create an inbound NAT pool for direct routed connectivity (not load balanced) toohello VMs in hello scale set via hello Load Balancer.</span></span> <span data-ttu-id="596b5-123">RDP를 사용 하 여 toodemonstrate 이므로 응용 프로그램에 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="596b5-123">This is toodemonstrate using RDP and may not be required in your application.</span></span>

```
$frontendpoolrangestart = 3360
$frontendpoolrangeend = 3370
$backendvmport = 3389
$inboundNatPool = New-AzureRmLoadBalancerInboundNatPoolConfig -Name $inboundNatPoolName -FrontendIPConfigurationId `
$frontend.Id -Protocol Tcp -FrontendPortRangeStart $frontendpoolrangestart -FrontendPortRangeEnd $frontendpoolrangeend -BackendPort $backendvmport;
```

<span data-ttu-id="596b5-124">Hello 부하 분산 규칙을 보여 줍니다 요청의 부하를 분산 포트 80을 이전 단계에서 hello 설정을 사용 하 여이 예제를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="596b5-124">Create hello Load Balanced Rule, this example shows load balancing port 80 requests, using hello settings from previous steps.</span></span>

```
$protocol = 'Tcp'
$feLBPort = 80
$beLBPort = 80

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name $lbruleName `
-FrontendIPConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -Protocol $protocol -FrontendPort $feLBPort -BackendPort $beLBPort `
-IdleTimeoutInMinutes 15 -EnableFloatingIP -LoadDistribution SourceIP -Verbose;
```

<span data-ttu-id="596b5-125">구성을 사용하여 부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="596b5-125">Create Load Balancer with configuration.</span></span>

```
$actualLb = New-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname -Location $loc `
-FrontendIpConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -LoadBalancingRule $lbrule -InboundNatPool $inboundNatPool -Verbose;
```

<span data-ttu-id="596b5-126">LB 설정을 확인 하십시오 부하 분산 된 포트 configs 참고 hello 크기 집합의 Vm hello까지 인바운드 NAT 규칙을 만들 표시 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="596b5-126">Check  LB settings, check load balanced port configs, note, you will not see Inbound NAT rules until hello VMs in hello scale set are created.</span></span>

```
$expectedLb = Get-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname
```

##### <a name="configure-and-create-hello-scale-set"></a><span data-ttu-id="596b5-127">구성 하 고 만들기 hello 크기 조정 설정</span><span class="sxs-lookup"><span data-stu-id="596b5-127">Configure and Create hello scale set</span></span>
<span data-ttu-id="596b5-128">Note 보여 주는 인프라 예제를 tooset 배포 방법과 배율 웹 트래픽 hello 크기 집합 하지만 hello 여기에서 지정 된 Vm 이미지에서 설치 된 모든 웹 서비스를 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="596b5-128">Note, this infrastructure example shows how tooset up distribute and scale web traffic across hello scale set, but hello VMs Images specified here do not have any web services installed.</span></span>

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

<span data-ttu-id="596b5-129">서브넷과 NIC tooLoad 분산 장치 바인딩</span><span class="sxs-lookup"><span data-stu-id="596b5-129">Bind NIC tooLoad Balancer and Subnet</span></span>

```
$ipCfg = New-AzureRmVmssIPConfig -Name 'nic' `
-LoadBalancerInboundNatPoolsId $actualLb.InboundNatPools[0].Id `
-LoadBalancerBackendAddressPoolsId $actualLb.BackendAddressPools[0].Id `
-SubnetId $subnetId;
```

<span data-ttu-id="596b5-130">크기 집합 구성 만들기</span><span class="sxs-lookup"><span data-stu-id="596b5-130">Create scale set Config</span></span>

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

<span data-ttu-id="596b5-131">크기 집합 구성 빌드</span><span class="sxs-lookup"><span data-stu-id="596b5-131">Build scale set configuration</span></span>

```
New-AzureRmVmss -ResourceGroupName $rgname -Name $vmssName -VirtualMachineScaleSet $vmss -Verbose;
```

<span data-ttu-id="596b5-132">이제 hello 크기 집합을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="596b5-132">Now you have created hello scale set.</span></span> <span data-ttu-id="596b5-133">연결 toohello를 테스트할 수 RDP를 사용 하 여이 예제는 개별 VM:</span><span class="sxs-lookup"><span data-stu-id="596b5-133">You can test connecting toohello individual VM using RDP in this example:</span></span>

```
VM0 : pubipmynewrgwu.westus.cloudapp.azure.com:3360
VM1 : pubipmynewrgwu.westus.cloudapp.azure.com:3361
VM2 : pubipmynewrgwu.westus.cloudapp.azure.com:3362
```
