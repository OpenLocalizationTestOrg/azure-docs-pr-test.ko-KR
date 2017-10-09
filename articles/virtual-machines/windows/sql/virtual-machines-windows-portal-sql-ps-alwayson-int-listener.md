---
title: "Microsoft Azure aaaConfigure 항상에서 가용성 그룹 수신기 – | Microsoft Docs"
description: "하나 이상의 IP 주소와 내부 부하 분산을 사용 하 여 hello Azure 리소스 관리자 모델에서 가용성 그룹 수신기를 구성 합니다."
services: virtual-machines
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: monicar
ms.assetid: 14b39cde-311c-4ddf-98f3-8694e01a7d3b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/22/2017
ms.author: mikeray
ms.openlocfilehash: 81edfe2c2ea536d8dcec466f36fccf8bc0e02c2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-one-or-more-always-on-availability-group-listeners---resource-manager"></a><span data-ttu-id="c4703-103">하나 이상의 Always On 가용성 그룹 수신기 구성 - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c4703-103">Configure one or more Always On availability group listeners - Resource Manager</span></span>
<span data-ttu-id="c4703-104">이 문서에서는 다음을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-104">This topic shows how to:</span></span>

* <span data-ttu-id="c4703-105">PowerShell cmdlet을 사용하여 SQL Server 가용성 그룹에 대한 내부 부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-105">Create an internal load balancer for SQL Server availability groups using PowerShell cmdlets.</span></span>
* <span data-ttu-id="c4703-106">여러 가용성 그룹에 대 한 추가 IP 주소 tooa 부하 분산을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-106">Add additional IP addresses tooa load balancer for more than one availability group.</span></span> 

<span data-ttu-id="c4703-107">가용성 그룹 수신기는 클라이언트가 연결할 toofor 데이터베이스 액세스는 가상 네트워크 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-107">An availability group listener is a virtual network name that clients connect toofor database access.</span></span> <span data-ttu-id="c4703-108">Azure 가상 컴퓨터에 부하 분산 장치는 hello 수신기에 대 한 hello IP 주소를 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-108">On Azure virtual machines, a load balancer holds hello IP address for hello listener.</span></span> <span data-ttu-id="c4703-109">hello 부하 분산 장치 경로 트래픽 toohello SQL Server 인스턴스의 hello 프로브 포트에서 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-109">hello load balancer routes traffic toohello instance of SQL Server that is listening on hello probe port.</span></span> <span data-ttu-id="c4703-110">일반적으로 가용성 그룹은 내부 부하 분산 장치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-110">Usually, an availability group uses an internal load balancer.</span></span> <span data-ttu-id="c4703-111">Azure 내부 부하 분산 장치는 하나 이상의 IP 주소를 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-111">An Azure internal load balancer can host one or many IP addresses.</span></span> <span data-ttu-id="c4703-112">각 IP 주소는 특정 프로브 포트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-112">Each IP address uses a specific probe port.</span></span> <span data-ttu-id="c4703-113">이 문서에서는 어떻게 toouse PowerShell toocreate 부하 분산 장치 또는 IP 주소 tooan 기존 SQL Server 가용성 그룹에 대 한 부하 분산 장치를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-113">This document shows how toouse PowerShell toocreate a load balancer, or add IP addresses tooan existing load balancer for SQL Server availability groups.</span></span> 

<span data-ttu-id="c4703-114">hello 기능 tooassign 여러 IP 주소 tooan 내부 부하 분산 장치 새 tooAzure 이며 리소스 관리자 모델에서 사용할 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-114">hello ability tooassign multiple IP addresses tooan internal load balancer is new tooAzure and is only available in Resource Manager model.</span></span> <span data-ttu-id="c4703-115">toocomplete toohave SQL Server 가용성 그룹 리소스 관리자 모델에서 Azure 가상 컴퓨터에 배포 해야이 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-115">toocomplete this task, you need toohave a SQL Server availability group deployed on Azure virtual machines in Resource Manager model.</span></span> <span data-ttu-id="c4703-116">SQL Server 가상 컴퓨터 둘 다 toohello 속해야 합니다. 동일한 가용성 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-116">Both SQL Server virtual machines must belong toohello same availability set.</span></span> <span data-ttu-id="c4703-117">Hello를 사용할 수 있습니다 [Microsoft 템플릿](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) tooautomatically Azure 리소스 관리자의 hello 가용성 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-117">You can use hello [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) tooautomatically create hello availability group in Azure Resource Manager.</span></span> <span data-ttu-id="c4703-118">이 서식 파일에는 자동으로 hello 내부 부하 분산 장치를 포함 하 여 hello 가용성 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-118">This template automatically creates hello availability group, including hello internal load balancer for you.</span></span> <span data-ttu-id="c4703-119">원하는 경우 [수동으로 Always On 가용성 그룹을 구성](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-119">If you prefer, you can [manually configure an Always On availability group](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span></span>

<span data-ttu-id="c4703-120">이 항목을 수행하려면 가용성 그룹이 이미 구성되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-120">This topic requires that your availability groups are already configured.</span></span>  

<span data-ttu-id="c4703-121">관련 항목은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-121">Related topics include:</span></span>

* [<span data-ttu-id="c4703-122">Azure VM의 Always On 가용성 그룹 구성(GUI)</span><span class="sxs-lookup"><span data-stu-id="c4703-122">Configure AlwaysOn Availability Groups in Azure VM (GUI)</span></span>](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [<span data-ttu-id="c4703-123">Azure 리소스 관리자 및 PowerShell을 사용하여 VNet-VNet 연결 구성</span><span class="sxs-lookup"><span data-stu-id="c4703-123">Configure a VNet-to-VNet connection by using Azure Resource Manager and PowerShell</span></span>](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

[!INCLUDE [Start your PowerShell session](../../../../includes/sql-vm-powershell.md)]

## <a name="configure-hello-windows-firewall"></a><span data-ttu-id="c4703-124">Hello Windows 방화벽 구성</span><span class="sxs-lookup"><span data-stu-id="c4703-124">Configure hello Windows Firewall</span></span>
<span data-ttu-id="c4703-125">Hello Windows 방화벽 tooallow SQL Server 액세스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-125">Configure hello Windows Firewall tooallow SQL Server access.</span></span> <span data-ttu-id="c4703-126">hello 방화벽 규칙 TCP 연결 toohello 포트 hello SQL Server 인스턴스 및 hello 수신기 프로브 여 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-126">hello firewall rules allow TCP connections toohello ports use by hello SQL Server instance, and hello listener probe.</span></span> <span data-ttu-id="c4703-127">자세한 지침은 [데이터베이스 엔진 액세스를 위해 Windows 방화벽 구성](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4703-127">For detailed instructions, see [Configure a Windows Firewall for Database Engine Access](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1).</span></span> <span data-ttu-id="c4703-128">Hello 프로브 포트 및 SQL Server 포트 hello에 대 한 인바운드 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-128">Create an inbound rule for hello SQL Server port and for hello probe port.</span></span>

## <a name="example-script-create-an-internal-load-balancer-with-powershell"></a><span data-ttu-id="c4703-129">예제 스크립트: PowerShell을 사용하여 내부 부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="c4703-129">Example Script: Create an internal load balancer with PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="c4703-130">Hello를 사용 하 여 가용성 그룹을 만든 경우 [Microsoft 템플릿](virtual-machines-windows-portal-sql-alwayson-availability-groups.md), hello 내부 부하 분산 장치 이미 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-130">If you created your availability group with hello [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md), hello internal load balancer was already created.</span></span> 
> 
> 

<span data-ttu-id="c4703-131">hello 다음 PowerShell 스크립트는 내부 부하 분산 장치, 구성 hello 부하 분산 규칙을 만들고 hello 부하 분산 장치에 대 한 IP 주소를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-131">hello following PowerShell script creates an internal load balancer, configures hello load balancing rules, and sets an IP address for hello load balancer.</span></span> <span data-ttu-id="c4703-132">toorun hello 스크립트를 Windows PowerShell ISE를 열고 hello 스크립트 hello 스크립트 창에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-132">toorun hello script, open Windows PowerShell ISE, and paste hello script in hello Script pane.</span></span> <span data-ttu-id="c4703-133">사용 하 여 `Login-AzureRMAccount` toolog tooPowerShell에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-133">Use `Login-AzureRMAccount` toolog in tooPowerShell.</span></span> <span data-ttu-id="c4703-134">여러 Azure 구독이 있으면 사용 하 여 `Select-AzureRmSubscription ` tooset hello 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-134">If you have multiple Azure subscriptions, use `Select-AzureRmSubscription ` tooset hello subscription.</span></span> 

```powershell
# Login-AzureRmAccount
# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>

$ResourceGroupName = "<Resource Group Name>" # Resource group name
$VNetName = "<Virtual Network Name>"         # Virtual network name
$SubnetName = "<Subnet Name>"                # Subnet name
$ILBName = "<Load Balancer Name>"            # ILB name
$Location = "<Azure Region>"                 # Azure location
$VMNames = "<VM1>","<VM2>"                   # Virtual machine names

$ILBIP = "<n.n.n.n>"                         # IP address
[int]$ListenerPort = "<nnnn>"                # AG listener port
[int]$ProbePort = "<nnnn>"                   # Probe port

$LBProbeName ="ILBPROBE_$ListenerPort"       # hello Load balancer Probe Object Name              
$LBConfigRuleName = "ILBCR_$ListenerPort"    # hello Load Balancer Rule Object Name

$FrontEndConfigurationName = "FE_SQLAGILB_1" # Object name for hello front-end configuration 
$BackEndConfigurationName ="BE_SQLAGILB_1"   # Object name for hello back-end configuration

$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName 

$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName 

$FEConfig = New-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.id

$BEConfig = New-AzureRMLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName 

$SQLHealthProbe = New-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -Protocol tcp -Port $ProbePort -IntervalInSeconds 15 -ProbeCount 2

$ILBRule = New-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig -BackendAddressPool $BEConfig -Probe $SQLHealthProbe -Protocol tcp -FrontendPort $ListenerPort -BackendPort $ListenerPort -LoadDistribution Default -EnableFloatingIP 

$ILB= New-AzureRmLoadBalancer -Location $Location -Name $ILBName -ResourceGroupName $ResourceGroupName -FrontendIpConfiguration $FEConfig -BackendAddressPool $BEConfig -LoadBalancingRule $ILBRule -Probe $SQLHealthProbe 

$bepool = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB 

foreach($VMName in $VMNames)
    {
        $VM = Get-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VMName 
        $NICName = ($vm.NetworkProfile.NetworkInterfaces.Id.split('/') | select -last 1)
        $NIC = Get-AzureRmNetworkInterface -name $NICName -ResourceGroupName $ResourceGroupName
        $NIC.IpConfigurations[0].LoadBalancerBackendAddressPools = $BEPool
        Set-AzureRmNetworkInterface -NetworkInterface $NIC
        start-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VM.Name 
    }
```

## <span data-ttu-id="c4703-135"><a name="Add-IP"></a>스크립트 예:는 IP 주소 tooan 기존 부하 분산 장치 추가 powershell</span><span class="sxs-lookup"><span data-stu-id="c4703-135"><a name="Add-IP"></a> Example script: Add an IP address tooan existing load balancer with PowerShell</span></span>
<span data-ttu-id="c4703-136">toouse 두 개 이상의 하나의 가용성 그룹에서 추가 IP 주소 toohello 부하 분산 장치를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-136">toouse more than one availability group, add an additional IP address toohello load balancer.</span></span> <span data-ttu-id="c4703-137">각 IP 주소에는 자체 부하 분산 규칙, 프로브 포트 및 프런트 엔드 포트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-137">Each IP address requires its own load balancing rule, probe port, and front port.</span></span>

<span data-ttu-id="c4703-138">hello 프런트 엔드 포트는 응용 프로그램 tooconnect toohello SQL Server 인스턴스를 사용 하는 hello 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-138">hello front-end port is hello port that applications use tooconnect toohello SQL Server instance.</span></span> <span data-ttu-id="c4703-139">다른 가용성 그룹을 사용 하 여 수에 대 한 IP 주소 hello 동일한 프런트 엔드 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-139">IP addresses for different availability groups can use hello same front-end port.</span></span>

> [!NOTE]
> <span data-ttu-id="c4703-140">SQL Server 가용성 그룹의 경우 각 IP 주소에 특정 프로브 포트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-140">For SQL Server availability groups, each IP address requires a specific probe port.</span></span> <span data-ttu-id="c4703-141">예를 들어 부하 분산 장치에 있는 하나의 IP 주소가 프로브 포트 59999를 사용하는 경우 해당 부하 분산 장치의 다른 IP 주소는 프로브 포트 59999를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-141">For example, if one IP address on a load balancer uses probe port 59999, no other IP addresses on that load balancer can use probe port 59999.</span></span>

* <span data-ttu-id="c4703-142">부하 분산 장치 제한에 대한 자세한 내용은 **네트워킹 제한 - Azure Resource Manager**에서 [부하 분산 장치당 개인 프런트 엔드 IP](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4703-142">For information about load balancer limits, see **Private front end IP per load balancer** under [Networking Limits - Azure Resource Manager](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits).</span></span>
* <span data-ttu-id="c4703-143">가용성 그룹 제한에 대한 자세한 내용은 [제한 사항(가용성 그룹)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4703-143">For information about availability group limits, see [Restrictions (Availability Groups)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG).</span></span>

<span data-ttu-id="c4703-144">hello 다음 스크립트 추가 새 IP 주소 tooan 기존 부하 분산 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-144">hello following script adds a new IP address tooan existing load balancer.</span></span> <span data-ttu-id="c4703-145">ILB hello hello 부하 분산 프런트 엔드 포트에 대 한 hello 수신기 포트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-145">hello ILB uses hello listener port for hello load balancing front-end port.</span></span> <span data-ttu-id="c4703-146">이 포트에서 수신 대기 중인 SQL Server hello 포트 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-146">This port can be hello port that SQL Server is listening on.</span></span> <span data-ttu-id="c4703-147">SQL Server의 기본 인스턴스의 경우 hello 포트는 1433입니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-147">For default instances of SQL Server, hello port is 1433.</span></span> <span data-ttu-id="c4703-148">hello 부하 분산 가용성 그룹에 대 한 규칙 부동 IP (직접 서버 반환) hello 백 엔드 포트 이므로 hello 동일 hello 프런트 엔드 포트와 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-148">hello load balancing rule for an availability group requires a floating IP (direct server return) so hello back-end port is hello same as hello front-end port.</span></span> <span data-ttu-id="c4703-149">사용자 환경에 대 한 hello 변수를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-149">Update hello variables for your environment.</span></span> 

```powershell
# Login-AzureRmAccount
# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>

$ResourceGroupName = "<ResourceGroup>"          # Resource group name
$VNetName = "<VirtualNetwork>"                  # Virtual network name
$SubnetName = "<Subnet>"                        # Subnet name
$ILBName = "<ILBName>"                          # ILB name                      

$ILBIP = "<n.n.n.n>"                            # IP address
[int]$ListenerPort = "<nnnn>"                   # AG listener port
[int]$ProbePort = "<nnnnn>"                     # Probe port 

$ILB = Get-AzureRmLoadBalancer -Name $ILBName -ResourceGroupName $ResourceGroupName 

$count = $ILB.FrontendIpConfigurations.Count+1
$FrontEndConfigurationName ="FE_SQLAGILB_$count"  

$LBProbeName = "ILBPROBE_$count"
$LBConfigrulename = "ILBCR_$count"

$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName 
$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName

$ILB | Add-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.Id 

$ILB | Add-AzureRmLoadBalancerProbeConfig -Name $LBProbeName  -Protocol Tcp -Port $Probeport -ProbeCount 2 -IntervalInSeconds 15  | Set-AzureRmLoadBalancer 

$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName

$FEConfig = get-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB

$SQLHealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

$BEConfig = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $ILB.BackendAddressPools[0].Name -LoadBalancer $ILB 

$ILB | Add-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig  -BackendAddressPool $BEConfig -Probe $SQLHealthProbe -Protocol tcp -FrontendPort  $ListenerPort -BackendPort $ListenerPort -LoadDistribution Default -EnableFloatingIP | Set-AzureRmLoadBalancer   
```

## <a name="configure-hello-listener"></a><span data-ttu-id="c4703-150">Hello 수신기 구성</span><span class="sxs-lookup"><span data-stu-id="c4703-150">Configure hello listener</span></span>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-hello-listener-port-in-sql-server-management-studio"></a><span data-ttu-id="c4703-151">SQL Server Management Studio에서 hello 수신기 포트를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-151">Set hello listener port in SQL Server Management Studio</span></span>

1. <span data-ttu-id="c4703-152">SQL Server Management Studio를 시작 하 고 toohello 주 복제본에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-152">Launch SQL Server Management Studio and connect toohello primary replica.</span></span>

1. <span data-ttu-id="c4703-153">너무 이동**AlwaysOn 고가용성** | **가용성 그룹** | **가용성 그룹 수신기**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-153">Navigate too**AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**.</span></span> 

1. <span data-ttu-id="c4703-154">이제 장애 조치 클러스터 관리자에서 만든 hello 수신기 이름이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-154">You should now see hello listener name that you created in Failover Cluster Manager.</span></span> <span data-ttu-id="c4703-155">Hello 수신기 이름을 마우스 오른쪽 단추로 클릭 하 고 클릭 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-155">Right-click hello listener name and click **Properties**.</span></span>

1. <span data-ttu-id="c4703-156">Hello에 **포트** 상자 이전 사용 $EndpointPort hello를 사용 하 여 hello 가용성 그룹 수신기에 대 한 hello 포트 번호를 지정 합니다 (1433 hello이 기본값 이었습니다)를 클릭 한 다음 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-156">In hello **Port** box, specify hello port number for hello availability group listener by using hello $EndpointPort you used earlier (1433 was hello default), then click **OK**.</span></span>

## <a name="test-hello-connection-toohello-listener"></a><span data-ttu-id="c4703-157">테스트 hello 연결 toohello 수신기</span><span class="sxs-lookup"><span data-stu-id="c4703-157">Test hello connection toohello listener</span></span>

<span data-ttu-id="c4703-158">tootest hello 연결:</span><span class="sxs-lookup"><span data-stu-id="c4703-158">tootest hello connection:</span></span>

1. <span data-ttu-id="c4703-159">RDP tooa SQL 서버 hello에 있는 동일한 가상 네트워크 구성 요소, 않도록 지정 되었으나 자체 hello 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-159">RDP tooa SQL Server that is in hello same virtual network, but does not own hello replica.</span></span> <span data-ttu-id="c4703-160">Hello 클러스터의 다른 SQL Server를 hello 수이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-160">This can be hello other SQL Server in hello cluster.</span></span>

1. <span data-ttu-id="c4703-161">사용 하 여 **sqlcmd** 유틸리티 tootest hello 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-161">Use **sqlcmd** utility tootest hello connection.</span></span> <span data-ttu-id="c4703-162">예를 들어 다음 스크립트는 hello 설정는 **sqlcmd** hello 수신기 Windows 인증을 통해 연결 toohello 주 복제본:</span><span class="sxs-lookup"><span data-stu-id="c4703-162">For example, hello following script establishes a **sqlcmd** connection toohello primary replica through hello listener with Windows authentication:</span></span>
   
    ```
    sqlmd -S <listenerName> -E
    ```
   
    <span data-ttu-id="c4703-163">Hello 수신기 포트를 사용 하는 이외의 경우 hello 기본 포트 (1433)를 hello 연결 문자열에 hello 포트를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-163">If hello listener is using a port other than hello default port (1433), specify hello port in hello connection string.</span></span> <span data-ttu-id="c4703-164">예를 들어 hello 다음 sqlcmd 명령을 연결 tooa 수신기 포트 1435에서:</span><span class="sxs-lookup"><span data-stu-id="c4703-164">For example, hello following sqlcmd command connects tooa listener at port 1435:</span></span> 
   
    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

<span data-ttu-id="c4703-165">hello SQLCMD 연결 toowhichever 인스턴스의 SQL Server 호스트 hello에 대 한 주 복제본을 자동으로 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-165">hello SQLCMD connection automatically connects toowhichever instance of SQL Server hosts hello primary replica.</span></span> 

> [!NOTE]
> <span data-ttu-id="c4703-166">지정한 hello 포트가 두 SQL Server의 hello 방화벽에서 열려 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-166">Make sure that hello port you specify is open on hello firewall of both SQL Servers.</span></span> <span data-ttu-id="c4703-167">두 서버 hello 있습니다를 사용 하는 TCP 포트에 대 한 인바운드 규칙을 필요로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-167">Both servers require an inbound rule for hello TCP port that you use.</span></span> <span data-ttu-id="c4703-168">자세한 내용은 [방화벽 규칙 추가 또는 편집](http://technet.microsoft.com/library/cc753558.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4703-168">See [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx) for more information.</span></span> 
> 
> 

## <a name="guidelines-and-limitations"></a><span data-ttu-id="c4703-169">지침 및 제한 사항</span><span class="sxs-lookup"><span data-stu-id="c4703-169">Guidelines and limitations</span></span>
<span data-ttu-id="c4703-170">내부 부하 분산 장치를 사용 하 여 Azure에서 가용성 그룹 수신기에 대 한 지침을 따라 참고 hello:</span><span class="sxs-lookup"><span data-stu-id="c4703-170">Note hello following guidelines on availability group listener in Azure using internal load balancer:</span></span>

* <span data-ttu-id="c4703-171">내부 부하 분산 장치,만 hello 내에서 hello 수신기가 액세스할 동일한 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-171">With an internal load balancer, you only access hello listener from within hello same virtual network.</span></span>


## <a name="for-more-information"></a><span data-ttu-id="c4703-172">Blob에 대한 자세한 내용은</span><span class="sxs-lookup"><span data-stu-id="c4703-172">For more information</span></span>
<span data-ttu-id="c4703-173">자세한 내용은 [수동으로 Azure VM의 Always On 가용성 그룹 구성](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4703-173">For more information, see [Configure Always On availability group in Azure VM manually](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span></span>

## <a name="powershell-cmdlets"></a><span data-ttu-id="c4703-174">PowerShell cmdlet</span><span class="sxs-lookup"><span data-stu-id="c4703-174">PowerShell cmdlets</span></span>
<span data-ttu-id="c4703-175">다음 PowerShell cmdlet toocreate Azure 가상 컴퓨터에 대 한 내부 부하 분산 장치는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-175">Use hello following PowerShell cmdlets toocreate an internal load balancer for Azure virtual machines.</span></span>

* <span data-ttu-id="c4703-176">[New-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt619450.aspx)는 부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-176">[New-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt619450.aspx) creates a load balancer.</span></span> 
* <span data-ttu-id="c4703-177">[New-AzureRMLoadBalancerFrontendIpConfig](http://msdn.microsoft.com/library/mt603510.aspx)는 부하 분산 장치에 대한 프런트 엔드 IP 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-177">[New-AzureRMLoadBalancerFrontendIpConfig](http://msdn.microsoft.com/library/mt603510.aspx) creates a front-end IP configuration for a load balancer.</span></span> 
* <span data-ttu-id="c4703-178">[New-AzureRmLoadBalancerRuleConfig](http://msdn.microsoft.com/library/mt619391.aspx)는 부하 분산 장치에 대한 규칙 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-178">[New-AzureRmLoadBalancerRuleConfig](http://msdn.microsoft.com/library/mt619391.aspx) creates a rule configuration for a load balancer.</span></span> 
* <span data-ttu-id="c4703-179">[New-AzureRmLoadBalancerBackendAddressPoolConfig](http://msdn.microsoft.com/library/mt603791.aspx)는 부하 분산 장치에 대한 백 엔드 주소 풀 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-179">[New-AzureRmLoadBalancerBackendAddressPoolConfig](http://msdn.microsoft.com/library/mt603791.aspx) creates a backend address pool configuration for a load balancer.</span></span> 
* <span data-ttu-id="c4703-180">[New-AzureRmLoadBalancerProbeConfig](http://msdn.microsoft.com/library/mt603847.aspx)는 부하 분산 장치에 대한 프로브 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-180">[New-AzureRmLoadBalancerProbeConfig](http://msdn.microsoft.com/library/mt603847.aspx) creates a probe configuration for a load balancer.</span></span>
* <span data-ttu-id="c4703-181">[Remove-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx)는 Azure 리소스 그룹에서 부하 분산 장치를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="c4703-181">[Remove-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx) removes a load balancer from an Azure resource group.</span></span>
