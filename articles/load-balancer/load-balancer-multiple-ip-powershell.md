---
title: "Azure에서 여러 IP 구성의 부하 분산 | Microsoft Docs"
description: "기본 및 보조 IP 구성에서 부하 분산."
services: load-balancer
documentationcenter: na
author: anavinahar
manager: narayan
editor: na
ms.assetid: 244907cd-b275-4494-aaf7-dcfc4d93edfe
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: annahar
ms.openlocfilehash: a8550519f094ca7afcd868a14b313337627f97d3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="load-balancing-on-multiple-ip-configurations-using-powershell"></a><span data-ttu-id="47fe2-103">PowerShell을 사용하여 여러 IP 구성의 부하 분산</span><span class="sxs-lookup"><span data-stu-id="47fe2-103">Load balancing on multiple IP configurations using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="47fe2-104">포털</span><span class="sxs-lookup"><span data-stu-id="47fe2-104">Portal</span></span>](load-balancer-multiple-ip.md)
> * [<span data-ttu-id="47fe2-105">CLI</span><span class="sxs-lookup"><span data-stu-id="47fe2-105">CLI</span></span>](load-balancer-multiple-ip-cli.md)
> * [<span data-ttu-id="47fe2-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="47fe2-106">PowerShell</span></span>](load-balancer-multiple-ip-powershell.md)

<span data-ttu-id="47fe2-107">이 문서에서는 보조 NIC(네트워크 인터페이스)에 여러 IP 주소가 있는 Azure Load Balancer를 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="47fe2-107">This article describes how to use Azure Load Balancer with multiple IP addresses on a secondary network interface (NIC).</span></span> <span data-ttu-id="47fe2-108">이 시나리오에는 Windows를 실행하는 VM이 둘 있고 각각 기본 및 보조 NIC가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47fe2-108">For this scenario, we have two VMs running Windows, each with a primary and a secondary NIC.</span></span> <span data-ttu-id="47fe2-109">보조 NIC에는 각각 두 가지 IP 구성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47fe2-109">Each of the secondary NICs have two IP configurations.</span></span> <span data-ttu-id="47fe2-110">각 VM은 contoso.com 및 fabrikam.com 웹 사이트를 둘 다 호스트합니다. 각 웹 사이트는 보조 NIC의 IP 구성 중 하나에 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="47fe2-110">Each VM hosts both websites contoso.com and fabrikam.com. Each website is bound to one of the IP configurations on the secondary NIC.</span></span> <span data-ttu-id="47fe2-111">Azure Load Balancer를 사용하여 웹 사이트의 각 IP 구성에 트래픽을 분산하기 위해 각 웹 사이트에 하나씩 두 개의 프런트 엔드 IP 주소를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="47fe2-111">We use Azure Load Balancer to expose two frontend IP addresses, one for each website, to distribute traffic to the respective IP configuration for the website.</span></span> <span data-ttu-id="47fe2-112">이 시나리오는 양 쪽 프런트 엔드는 물론 양쪽 백 엔드 풀 IP 주소에 동일한 포트 번호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="47fe2-112">This scenario uses the same port number across both frontends, as well as both backend pool IP addresses.</span></span>

![LB 시나리오 이미지](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-to-load-balance-on-multiple-ip-configurations"></a><span data-ttu-id="47fe2-114">여러 IP 구성의 부하를 분산하는 단계</span><span class="sxs-lookup"><span data-stu-id="47fe2-114">Steps to load balance on multiple IP configurations</span></span>

<span data-ttu-id="47fe2-115">아래 단계에 따라 이 문서에 설명된 시나리오를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="47fe2-115">Follow the steps below to achieve the scenario outlined in this article:</span></span>

1. <span data-ttu-id="47fe2-116">Azure PowerShell을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="47fe2-116">Install Azure PowerShell.</span></span> <span data-ttu-id="47fe2-117">최신 버전의 Azure PowerShell 설치, 구독 선택, 자신의 계정에 로그인하는 방법에 대해서는 [Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47fe2-117">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for information about installing the latest version of Azure PowerShell, selecting your subscription, and signing in to your account.</span></span>
2. <span data-ttu-id="47fe2-118">다음 설정을 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="47fe2-118">Create a resource group using the following settings:</span></span>

    ```powershell
    $location = "westcentralus".
    $myResourceGroup = "contosofabrikam"
    ```

    <span data-ttu-id="47fe2-119">자세한 내용은 [리소스 그룹 만들기](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)의 2단계를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47fe2-119">For more information, see Step 2 of [Create a Resource Group](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

3. <span data-ttu-id="47fe2-120">VM을 포함할 [가용성 집합을 만듭니다](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="47fe2-120">[Create an Availability Set](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json) to contain your VMs.</span></span> <span data-ttu-id="47fe2-121">이 시나리오에서는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="47fe2-121">For this scenario, use the following command:</span></span>

    ```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset" -Location "West Central US"
    ```

4. <span data-ttu-id="47fe2-122">NIC가 하나인 VM 만들기를 준비하려면 [Windows VM 만들기](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)에 있는 3 ~ 5단계의 지침을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="47fe2-122">Follow instructions steps 3 through 5 in [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) article to prepare the creation of a VM with a single NIC.</span></span> <span data-ttu-id="47fe2-123">6.1단계를 실행하고 6.2단계 대신 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="47fe2-123">Execute step 6.1, and use the following instead of step 6.2:</span></span>

    ```powershell
    $availset = Get-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset"
    New-AzureRmVMConfig -VMName "VM1" -VMSize "Standard_DS1_v2" -AvailabilitySetId $availset.Id
    ```

    <span data-ttu-id="47fe2-124">그런 다음 [Windows VM 만들기](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)의 6.3 ~ 6.8단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="47fe2-124">Then complete [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) steps 6.3 through 6.8.</span></span>

5. <span data-ttu-id="47fe2-125">각각의 VM에 두 번째 IP 구성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="47fe2-125">Add a second IP configuration to each of the VMs.</span></span> <span data-ttu-id="47fe2-126">[가상 컴퓨터에 여러 IP 주소 할당](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add) 문서의 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="47fe2-126">Follow the instructions in [Assign multiple IP addresses to virtual machines](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add) article.</span></span> <span data-ttu-id="47fe2-127">다음 구성 설정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="47fe2-127">Use the following configuration settings:</span></span>

    ```powershell
    $NicName = "VM1-NIC2"
    $RgName = "contosofabrikam"
    $NicLocation = "West Central US"
    $IPConfigName4 = "VM1-ipconfig2"
    $Subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "mySubnet" -VirtualNetwork $myVnet
    ```

    <span data-ttu-id="47fe2-128">이 자습서의 경우 보조 IP 구성을 공용 IP와 연결할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="47fe2-128">You do not need to associate the secondary IP configurations with public IPs for the purpose of this tutorial.</span></span> <span data-ttu-id="47fe2-129">명령을 편집하여 공용 IP 연결 부분을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="47fe2-129">Edit the command to remove the public IP association part.</span></span>

6. <span data-ttu-id="47fe2-130">VM2에 대해 4 ~ 6단계를 다시 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="47fe2-130">Complete steps 4 through 6 of this article again for VM2.</span></span> <span data-ttu-id="47fe2-131">이 단계를 수행할 때 VM 이름을 VM2로 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47fe2-131">Be sure to replace the VM name to VM2 when doing this.</span></span> <span data-ttu-id="47fe2-132">두 번째 VM에 대해 가상 네트워크를 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="47fe2-132">Note that you do not need to create a virtual network for the second VM.</span></span> <span data-ttu-id="47fe2-133">사용 사례를 기반으로 새 서브넷을 만들거나 만들지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47fe2-133">You may or may not create a new subnet based on your use case.</span></span>

7. <span data-ttu-id="47fe2-134">두 개의 공용 IP 주소를 만들고 다음과 같이 적절한 변수에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="47fe2-134">Create two public IP addresses and store them in the appropriate variables as shown:</span></span>

    ```powershell
    $publicIP1 = New-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel contoso
    $publicIP2 = New-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel fabrikam

    $publicIP1 = Get-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam
    $publicIP2 = Get-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam
    ```

8. <span data-ttu-id="47fe2-135">두 개의 프런트 엔드 IP 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="47fe2-135">Create two frontend IP configurations:</span></span>

    ```powershell
    $frontendIP1 = New-AzureRmLoadBalancerFrontendIpConfig -Name contosofe -PublicIpAddress $publicIP1
    $frontendIP2 = New-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2
    ```

9. <span data-ttu-id="47fe2-136">백 엔드 주소 풀, 프로브, 부하 분산 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="47fe2-136">Create your backend address pools, a probe, and your load balancing rules:</span></span>

    ```powershell
    $beaddresspool1 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name contosopool
    $beaddresspool2 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool

    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HTTP -RequestPath 'index.html' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

    $lbrule1 = New-AzureRmLoadBalancerRuleConfig -Name HTTPc -FrontendIpConfiguration $frontendIP1 -BackendAddressPool $beaddresspool1 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    $lbrule2 = New-AzureRmLoadBalancerRuleConfig -Name HTTPf -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

10. <span data-ttu-id="47fe2-137">이러한 리소스를 만들었으면 부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="47fe2-137">Once you have these resources created, create your load balancer:</span></span>

    ```powershell
    $mylb = New-AzureRmLoadBalancer -ResourceGroupName contosofabrikam -Name mylb -Location 'West Central US' -FrontendIpConfiguration $frontendIP1 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

11. <span data-ttu-id="47fe2-138">두 번째 백 엔드 주소 풀 및 프런트 엔드 IP 구성을 새로 만든 부하 분산 장치에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="47fe2-138">Add the second backend address pool and frontend IP configuration to your newly created load balancer:</span></span>

    ```powershell
    $mylb = Get-AzureRmLoadBalancer -Name "mylb" -ResourceGroupName $myResourceGroup | Add-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool | Set-AzureRmLoadBalancer

    $mylb | Add-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2 | Set-AzureRmLoadBalancer
    
    Add-AzureRmLoadBalancerRuleConfig -Name HTTP -LoadBalancer $mylb -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80 | Set-AzureRmLoadBalancer
    ```

12. <span data-ttu-id="47fe2-139">아래 명령은 NIC를 가져온 다음 보조 NIC 각각의 IP 구성 두 개를 부하 분산 장치의 백 엔드 주소 풀에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="47fe2-139">The commands below get the NICs and then add both IP configurations of each secondary NIC to the backend address pool of the load balancer:</span></span>

    ```powershell
    $nic1 = Get-AzureRmNetworkInterface -Name "VM1-NIC2" -ResourceGroupName "MyResourcegroup";
    $nic2 = Get-AzureRmNetworkInterface -Name "VM2-NIC2" -ResourceGroupName "MyResourcegroup";

    $nic1.IpConfigurations[0].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[0]);
    $nic1.IpConfigurations[1].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[1]);
    $nic2.IpConfigurations[0].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[0]);
    $nic2.IpConfigurations[1].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[1]);

    $mylb = $mylb | Set-AzureRmLoadBalancer

    $nic1 | Set-AzureRmNetworkInterface
    $nic2 | Set-AzureRmNetworkInterface
    ```

13. <span data-ttu-id="47fe2-140">마지막으로 DNS 리소스 레코드가 부하 분산 장치의 각 프런트 엔드 IP 주소를 가리키도록 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47fe2-140">Finally, you must configure DNS resource records to point to the respective frontend IP address of the Load Balancer.</span></span> <span data-ttu-id="47fe2-141">도메인을 Azure DNS에 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47fe2-141">You may host your domains in Azure DNS.</span></span> <span data-ttu-id="47fe2-142">Load Balancer와 Azure DNS를 사용하는 방법에 대한 자세한 내용은 [다른 Azure 서비스와 함께 Azure DNS 사용](../dns/dns-for-azure-services.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47fe2-142">For more information about using Azure DNS with Load Balancer, see [Using Azure DNS with other Azure services](../dns/dns-for-azure-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="47fe2-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="47fe2-143">Next steps</span></span>
- <span data-ttu-id="47fe2-144">Azure에서 부하 분산 서비스를 결합하는 방법에 대한 자세한 내용은 [Azure에서 부하 분산 서비스 사용](../traffic-manager/traffic-manager-load-balancing-azure.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47fe2-144">Learn more about how to combine load balancing services in Azure in [Using load-balancing services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span></span>
- <span data-ttu-id="47fe2-145">[Azure Load Balancer에 대한 로그 분석](../load-balancer/load-balancer-monitor-log.md)을 통해 Azure에서 부하 분산 장치를 관리하고 문제를 해결하는 데 다양한 유형의 로그를 사용하는 방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="47fe2-145">Learn how you can use different types of logs in Azure to manage and troubleshoot load balancer in [Log analytics for Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span></span>
