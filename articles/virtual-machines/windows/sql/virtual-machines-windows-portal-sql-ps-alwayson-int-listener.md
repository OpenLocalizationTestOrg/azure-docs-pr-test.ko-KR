---
title: "Always On 가용성 그룹 수신기 구성 - Microsoft Azure | Microsoft 문서"
description: "하나 이상의 IP 주소를 갖는 내부 부하 분산 장치를 사용하여 Azure Resource Manager 모델에서 가용성 그룹 수신기를 구성합니다."
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
ms.openlocfilehash: 74fa1e4c9cfa608a9a385f3dd82a0599fbcc421c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-one-or-more-always-on-availability-group-listeners---resource-manager"></a><span data-ttu-id="af8fa-103">하나 이상의 Always On 가용성 그룹 수신기 구성 - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="af8fa-103">Configure one or more Always On availability group listeners - Resource Manager</span></span>
<span data-ttu-id="af8fa-104">이 문서에서는 다음을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-104">This topic shows how to:</span></span>

* <span data-ttu-id="af8fa-105">PowerShell cmdlet을 사용하여 SQL Server 가용성 그룹에 대한 내부 부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-105">Create an internal load balancer for SQL Server availability groups using PowerShell cmdlets.</span></span>
* <span data-ttu-id="af8fa-106">둘 이상의 가용성 그룹에 대한 추가 IP 주소를 부하 분산 장치에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-106">Add additional IP addresses to a load balancer for more than one availability group.</span></span> 

<span data-ttu-id="af8fa-107">가용성 그룹 수신기는 데이터베이스 액세스를 위해 클라이언트에서 연결하는 가상 네트워크 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-107">An availability group listener is a virtual network name that clients connect to for database access.</span></span> <span data-ttu-id="af8fa-108">Azure 가상 컴퓨터에서 부하 분산 장치는 수신기에 대한 IP 주소를 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-108">On Azure virtual machines, a load balancer holds the IP address for the listener.</span></span> <span data-ttu-id="af8fa-109">부하 분산 장치는 프로브 포트에서 수신 대기하는 SQL Server의 인스턴스로 트래픽을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-109">The load balancer routes traffic to the instance of SQL Server that is listening on the probe port.</span></span> <span data-ttu-id="af8fa-110">일반적으로 가용성 그룹은 내부 부하 분산 장치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-110">Usually, an availability group uses an internal load balancer.</span></span> <span data-ttu-id="af8fa-111">Azure 내부 부하 분산 장치는 하나 이상의 IP 주소를 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-111">An Azure internal load balancer can host one or many IP addresses.</span></span> <span data-ttu-id="af8fa-112">각 IP 주소는 특정 프로브 포트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-112">Each IP address uses a specific probe port.</span></span> <span data-ttu-id="af8fa-113">이 문서에서는 PowerShell을 사용하여 부하 분산 장치를 만들거나 SQL Server 가용성 그룹에 대한 기존 부하 분산 장치에 IP 주소를 추가하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-113">This document shows how to use PowerShell to create a load balancer, or add IP addresses to an existing load balancer for SQL Server availability groups.</span></span> 

<span data-ttu-id="af8fa-114">내부 부하 분산 장치에 여러 IP 주소를 할당하는 기능은 Azure에 새로 추가되었으며 Resource Manager 모델에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-114">The ability to assign multiple IP addresses to an internal load balancer is new to Azure and is only available in Resource Manager model.</span></span> <span data-ttu-id="af8fa-115">이 작업을 완료하려면 Resource Manager 모델의 Azure 가상 컴퓨터에 SQL Server 가용성 그룹이 배포되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-115">To complete this task, you need to have a SQL Server availability group deployed on Azure virtual machines in Resource Manager model.</span></span> <span data-ttu-id="af8fa-116">두 SQL Server 가상 컴퓨터는 동일한 가용성 집합에 속해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-116">Both SQL Server virtual machines must belong to the same availability set.</span></span> <span data-ttu-id="af8fa-117">[Microsoft 템플릿](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)을 사용하여 Azure Resource Manager에서 가용성 그룹을 자동으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-117">You can use the [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) to automatically create the availability group in Azure Resource Manager.</span></span> <span data-ttu-id="af8fa-118">이 템플릿은 내부 부하 분산 장치를 포함하는 가용성 그룹을 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-118">This template automatically creates the availability group, including the internal load balancer for you.</span></span> <span data-ttu-id="af8fa-119">원하는 경우 [수동으로 Always On 가용성 그룹을 구성](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-119">If you prefer, you can [manually configure an Always On availability group](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span></span>

<span data-ttu-id="af8fa-120">이 항목을 수행하려면 가용성 그룹이 이미 구성되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-120">This topic requires that your availability groups are already configured.</span></span>  

<span data-ttu-id="af8fa-121">관련 항목은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-121">Related topics include:</span></span>

* [<span data-ttu-id="af8fa-122">Azure VM의 Always On 가용성 그룹 구성(GUI)</span><span class="sxs-lookup"><span data-stu-id="af8fa-122">Configure AlwaysOn Availability Groups in Azure VM (GUI)</span></span>](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [<span data-ttu-id="af8fa-123">Azure 리소스 관리자 및 PowerShell을 사용하여 VNet-VNet 연결 구성</span><span class="sxs-lookup"><span data-stu-id="af8fa-123">Configure a VNet-to-VNet connection by using Azure Resource Manager and PowerShell</span></span>](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

[!INCLUDE [Start your PowerShell session](../../../../includes/sql-vm-powershell.md)]

## <a name="configure-the-windows-firewall"></a><span data-ttu-id="af8fa-124">Windows 방화벽 구성</span><span class="sxs-lookup"><span data-stu-id="af8fa-124">Configure the Windows Firewall</span></span>
<span data-ttu-id="af8fa-125">SQL Server 액세스를 허용하도록 Windows 방화벽을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-125">Configure the Windows Firewall to allow SQL Server access.</span></span> <span data-ttu-id="af8fa-126">방화벽 규칙에서 SQL Server 인스턴스 및 수신기 프로브에서 사용하는 포트에 TCP 연결을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-126">The firewall rules allow TCP connections to the ports use by the SQL Server instance, and the listener probe.</span></span> <span data-ttu-id="af8fa-127">자세한 지침은 [데이터베이스 엔진 액세스를 위해 Windows 방화벽 구성](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af8fa-127">For detailed instructions, see [Configure a Windows Firewall for Database Engine Access](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1).</span></span> <span data-ttu-id="af8fa-128">SQL Server 포트 및 프로브 포트에 대한 인바운드 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-128">Create an inbound rule for the SQL Server port and for the probe port.</span></span>

## <a name="example-script-create-an-internal-load-balancer-with-powershell"></a><span data-ttu-id="af8fa-129">예제 스크립트: PowerShell을 사용하여 내부 부하 분산 장치 만들기</span><span class="sxs-lookup"><span data-stu-id="af8fa-129">Example Script: Create an internal load balancer with PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="af8fa-130">[Microsoft 템플릿](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)으로 가용성 그룹을 만든 경우 내부 부하 분산 장치는 이미 만들어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-130">If you created your availability group with the [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md), the internal load balancer was already created.</span></span> 
> 
> 

<span data-ttu-id="af8fa-131">다음 PowerShell 스크립트는 내부 부하 분산 장치를 만들고, 부하 분산 규칙을 구성하고, 부하 분산 장치에 대한 IP 주소를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-131">The following PowerShell script creates an internal load balancer, configures the load balancing rules, and sets an IP address for the load balancer.</span></span> <span data-ttu-id="af8fa-132">이 스크립트를 실행하려면 Windows PowerShell ISE를 열고 스크립트 창으로 스크립트를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-132">To run the script, open Windows PowerShell ISE, and paste the script in the Script pane.</span></span> <span data-ttu-id="af8fa-133">`Login-AzureRMAccount`를 사용하여 PowerShell에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-133">Use `Login-AzureRMAccount` to log in to PowerShell.</span></span> <span data-ttu-id="af8fa-134">여러 Azure 구독이 있는 경우 `Select-AzureRmSubscription ` 사용하여 구독을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-134">If you have multiple Azure subscriptions, use `Select-AzureRmSubscription ` to set the subscription.</span></span> 

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

$LBProbeName ="ILBPROBE_$ListenerPort"       # The Load balancer Probe Object Name              
$LBConfigRuleName = "ILBCR_$ListenerPort"    # The Load Balancer Rule Object Name

$FrontEndConfigurationName = "FE_SQLAGILB_1" # Object name for the front-end configuration 
$BackEndConfigurationName ="BE_SQLAGILB_1"   # Object name for the back-end configuration

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

## <span data-ttu-id="af8fa-135"><a name="Add-IP"></a> 예제 스크립트: PowerShell을 사용하여 기존 부하 분산 장치에 IP 주소 추가</span><span class="sxs-lookup"><span data-stu-id="af8fa-135"><a name="Add-IP"></a> Example script: Add an IP address to an existing load balancer with PowerShell</span></span>
<span data-ttu-id="af8fa-136">둘 이상의 가용성 그룹을 사용하려면 추가 IP 주소를 부하 분산 장치에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-136">To use more than one availability group, add an additional IP address to the load balancer.</span></span> <span data-ttu-id="af8fa-137">각 IP 주소에는 자체 부하 분산 규칙, 프로브 포트 및 프런트 엔드 포트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-137">Each IP address requires its own load balancing rule, probe port, and front port.</span></span>

<span data-ttu-id="af8fa-138">프런트 엔드 포트는 응용 프로그램이 SQL Server 인스턴스에 연결하는 데 사용하는 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-138">The front-end port is the port that applications use to connect to the SQL Server instance.</span></span> <span data-ttu-id="af8fa-139">다른 가용성 그룹에 대한 IP 주소는 동일한 프런트 엔드 포트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-139">IP addresses for different availability groups can use the same front-end port.</span></span>

> [!NOTE]
> <span data-ttu-id="af8fa-140">SQL Server 가용성 그룹의 경우 각 IP 주소에 특정 프로브 포트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-140">For SQL Server availability groups, each IP address requires a specific probe port.</span></span> <span data-ttu-id="af8fa-141">예를 들어 부하 분산 장치에 있는 하나의 IP 주소가 프로브 포트 59999를 사용하는 경우 해당 부하 분산 장치의 다른 IP 주소는 프로브 포트 59999를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-141">For example, if one IP address on a load balancer uses probe port 59999, no other IP addresses on that load balancer can use probe port 59999.</span></span>

* <span data-ttu-id="af8fa-142">부하 분산 장치 제한에 대한 자세한 내용은 **네트워킹 제한 - Azure Resource Manager**에서 [부하 분산 장치당 개인 프런트 엔드 IP](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af8fa-142">For information about load balancer limits, see **Private front end IP per load balancer** under [Networking Limits - Azure Resource Manager](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits).</span></span>
* <span data-ttu-id="af8fa-143">가용성 그룹 제한에 대한 자세한 내용은 [제한 사항(가용성 그룹)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af8fa-143">For information about availability group limits, see [Restrictions (Availability Groups)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG).</span></span>

<span data-ttu-id="af8fa-144">다음 스크립트는 기존 부하 분산 장치에 새 IP 주소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-144">The following script adds a new IP address to an existing load balancer.</span></span> <span data-ttu-id="af8fa-145">ILB는 부하 분산 프런트 엔드 포트에 대해 수신기 포트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-145">The ILB uses the listener port for the load balancing front-end port.</span></span> <span data-ttu-id="af8fa-146">이 포트는 SQL Server에서 수신 대기 중인 포트일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-146">This port can be the port that SQL Server is listening on.</span></span> <span data-ttu-id="af8fa-147">SQL Server의 기본 인스턴스의 경우 포트는 1433입니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-147">For default instances of SQL Server, the port is 1433.</span></span> <span data-ttu-id="af8fa-148">가용성 그룹에 대한 부하 분산 규칙에는 부동 IP(Direct Server Return)가 필요하므로 백 엔드 포트는 프런트 엔드 포트와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-148">The load balancing rule for an availability group requires a floating IP (direct server return) so the back-end port is the same as the front-end port.</span></span> <span data-ttu-id="af8fa-149">사용자 환경에 맞게 변수를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-149">Update the variables for your environment.</span></span> 

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

## <a name="configure-the-listener"></a><span data-ttu-id="af8fa-150">수신기 구성</span><span class="sxs-lookup"><span data-stu-id="af8fa-150">Configure the listener</span></span>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-the-listener-port-in-sql-server-management-studio"></a><span data-ttu-id="af8fa-151">SQL Server Management Studio에서 수신기 포트 설정</span><span class="sxs-lookup"><span data-stu-id="af8fa-151">Set the listener port in SQL Server Management Studio</span></span>

1. <span data-ttu-id="af8fa-152">SQL Server Management Studio를 시작하고 주 복제본에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-152">Launch SQL Server Management Studio and connect to the primary replica.</span></span>

1. <span data-ttu-id="af8fa-153">**AlwaysOn 고가용성** | **가용성 그룹** | **가용성 그룹 수신기**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-153">Navigate to **AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**.</span></span> 

1. <span data-ttu-id="af8fa-154">이제 장애 조치(Failover) 클러스터 관리자에서 만든 수신기 이름이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-154">You should now see the listener name that you created in Failover Cluster Manager.</span></span> <span data-ttu-id="af8fa-155">수신기 이름을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-155">Right-click the listener name and click **Properties**.</span></span>

1. <span data-ttu-id="af8fa-156">**포트** 상자에서 이전에 사용한 $EndpointPort(1433이 기본값임)를 사용하여 가용성 그룹 수신기에 대한 포트 번호를 지정한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-156">In the **Port** box, specify the port number for the availability group listener by using the $EndpointPort you used earlier (1433 was the default), then click **OK**.</span></span>

## <a name="test-the-connection-to-the-listener"></a><span data-ttu-id="af8fa-157">수신기에 대한 연결 테스트</span><span class="sxs-lookup"><span data-stu-id="af8fa-157">Test the connection to the listener</span></span>

<span data-ttu-id="af8fa-158">연결을 테스트하려면</span><span class="sxs-lookup"><span data-stu-id="af8fa-158">To test the connection:</span></span>

1. <span data-ttu-id="af8fa-159">동일한 가상 네트워크에 있지만 복제본을 소유하지 않는 SQL Server로 RDP합니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-159">RDP to a SQL Server that is in the same virtual network, but does not own the replica.</span></span> <span data-ttu-id="af8fa-160">클러스터의 다른 SQL Server가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-160">This can be the other SQL Server in the cluster.</span></span>

1. <span data-ttu-id="af8fa-161">**sqlcmd** 유틸리티를 사용하여 연결을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-161">Use **sqlcmd** utility to test the connection.</span></span> <span data-ttu-id="af8fa-162">예를 들어 다음 스크립트는 Windows 인증을 사용하는 수신기를 통해 주 복제본에 대한 **sqlcmd** 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-162">For example, the following script establishes a **sqlcmd** connection to the primary replica through the listener with Windows authentication:</span></span>
   
    ```
    sqlmd -S <listenerName> -E
    ```
   
    <span data-ttu-id="af8fa-163">수신기가 기본 포트(1433) 이외의 포트를 사용하는 경우 연결 문자열에서 포트를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-163">If the listener is using a port other than the default port (1433), specify the port in the connection string.</span></span> <span data-ttu-id="af8fa-164">예를 들어 다음 sqlcmd 명령은 포트 1435에서 수신기에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-164">For example, the following sqlcmd command connects to a listener at port 1435:</span></span> 
   
    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

<span data-ttu-id="af8fa-165">SQLCMD 연결은 주 복제본을 호스트하는 SQL Server 인스턴스에 자동으로 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-165">The SQLCMD connection automatically connects to whichever instance of SQL Server hosts the primary replica.</span></span> 

> [!NOTE]
> <span data-ttu-id="af8fa-166">지정한 포트가 두 SQL Server의 방화벽에서 열려 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-166">Make sure that the port you specify is open on the firewall of both SQL Servers.</span></span> <span data-ttu-id="af8fa-167">두 서버 모두 사용하는 TCP 포트에 대한 인바운드 규칙이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-167">Both servers require an inbound rule for the TCP port that you use.</span></span> <span data-ttu-id="af8fa-168">자세한 내용은 [방화벽 규칙 추가 또는 편집](http://technet.microsoft.com/library/cc753558.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af8fa-168">See [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx) for more information.</span></span> 
> 
> 

## <a name="guidelines-and-limitations"></a><span data-ttu-id="af8fa-169">지침 및 제한 사항</span><span class="sxs-lookup"><span data-stu-id="af8fa-169">Guidelines and limitations</span></span>
<span data-ttu-id="af8fa-170">내부 부하 분산 장치를 사용하는 Azure에서는 가용성 그룹 수신기에 다음과 같은 지침이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-170">Note the following guidelines on availability group listener in Azure using internal load balancer:</span></span>

* <span data-ttu-id="af8fa-171">내부 부하 분산 장치를 사용할 경우 동일한 가상 네트워크 내에서만 수신기에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-171">With an internal load balancer, you only access the listener from within the same virtual network.</span></span>


## <a name="for-more-information"></a><span data-ttu-id="af8fa-172">Blob에 대한 자세한 내용은</span><span class="sxs-lookup"><span data-stu-id="af8fa-172">For more information</span></span>
<span data-ttu-id="af8fa-173">자세한 내용은 [수동으로 Azure VM의 Always On 가용성 그룹 구성](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af8fa-173">For more information, see [Configure Always On availability group in Azure VM manually](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span></span>

## <a name="powershell-cmdlets"></a><span data-ttu-id="af8fa-174">PowerShell cmdlet</span><span class="sxs-lookup"><span data-stu-id="af8fa-174">PowerShell cmdlets</span></span>
<span data-ttu-id="af8fa-175">다음 PowerShell cmdlet을 사용하여 Azure 가상 컴퓨터에 대한 내부 부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-175">Use the following PowerShell cmdlets to create an internal load balancer for Azure virtual machines.</span></span>

* <span data-ttu-id="af8fa-176">[New-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt619450.aspx)는 부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-176">[New-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt619450.aspx) creates a load balancer.</span></span> 
* <span data-ttu-id="af8fa-177">[New-AzureRMLoadBalancerFrontendIpConfig](http://msdn.microsoft.com/library/mt603510.aspx)는 부하 분산 장치에 대한 프런트 엔드 IP 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-177">[New-AzureRMLoadBalancerFrontendIpConfig](http://msdn.microsoft.com/library/mt603510.aspx) creates a front-end IP configuration for a load balancer.</span></span> 
* <span data-ttu-id="af8fa-178">[New-AzureRmLoadBalancerRuleConfig](http://msdn.microsoft.com/library/mt619391.aspx)는 부하 분산 장치에 대한 규칙 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-178">[New-AzureRmLoadBalancerRuleConfig](http://msdn.microsoft.com/library/mt619391.aspx) creates a rule configuration for a load balancer.</span></span> 
* <span data-ttu-id="af8fa-179">[New-AzureRmLoadBalancerBackendAddressPoolConfig](http://msdn.microsoft.com/library/mt603791.aspx)는 부하 분산 장치에 대한 백 엔드 주소 풀 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-179">[New-AzureRmLoadBalancerBackendAddressPoolConfig](http://msdn.microsoft.com/library/mt603791.aspx) creates a backend address pool configuration for a load balancer.</span></span> 
* <span data-ttu-id="af8fa-180">[New-AzureRmLoadBalancerProbeConfig](http://msdn.microsoft.com/library/mt603847.aspx)는 부하 분산 장치에 대한 프로브 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-180">[New-AzureRmLoadBalancerProbeConfig](http://msdn.microsoft.com/library/mt603847.aspx) creates a probe configuration for a load balancer.</span></span>
* <span data-ttu-id="af8fa-181">[Remove-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx)는 Azure 리소스 그룹에서 부하 분산 장치를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="af8fa-181">[Remove-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx) removes a load balancer from an Azure resource group.</span></span>
