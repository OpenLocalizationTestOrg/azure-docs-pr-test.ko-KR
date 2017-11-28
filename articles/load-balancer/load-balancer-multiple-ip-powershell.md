---
title: "Azure에서 여러 IP 구성에서 분산 aaaLoad | Microsoft Docs"
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
ms.openlocfilehash: fe1cdb317350942ff759229491c2025e98dd24a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balancing-on-multiple-ip-configurations-using-powershell"></a><span data-ttu-id="75749-103">PowerShell을 사용하여 여러 IP 구성의 부하 분산</span><span class="sxs-lookup"><span data-stu-id="75749-103">Load balancing on multiple IP configurations using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="75749-104">포털</span><span class="sxs-lookup"><span data-stu-id="75749-104">Portal</span></span>](load-balancer-multiple-ip.md)
> * [<span data-ttu-id="75749-105">CLI</span><span class="sxs-lookup"><span data-stu-id="75749-105">CLI</span></span>](load-balancer-multiple-ip-cli.md)
> * [<span data-ttu-id="75749-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="75749-106">PowerShell</span></span>](load-balancer-multiple-ip-powershell.md)

<span data-ttu-id="75749-107">이 문서에서는 Azure 부하 분산 장치에서 여러 ip toouse 보조 네트워크 인터페이스 (NIC)에서 해결 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="75749-107">This article describes how toouse Azure Load Balancer with multiple IP addresses on a secondary network interface (NIC).</span></span> <span data-ttu-id="75749-108">이 시나리오에는 Windows를 실행하는 VM이 둘 있고 각각 기본 및 보조 NIC가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75749-108">For this scenario, we have two VMs running Windows, each with a primary and a secondary NIC.</span></span> <span data-ttu-id="75749-109">각 보조 hello Nic가 두 개의 IP 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="75749-109">Each of hello secondary NICs have two IP configurations.</span></span> <span data-ttu-id="75749-110">각 VM은 contoso.com 및 fabrikam.com 웹 사이트를 둘 다 호스트합니다. 각 웹 사이트는 hello 보조 NIC에서 hello IP 구성의 바인딩된 tooone</span><span class="sxs-lookup"><span data-stu-id="75749-110">Each VM hosts both websites contoso.com and fabrikam.com. Each website is bound tooone of hello IP configurations on hello secondary NIC.</span></span> <span data-ttu-id="75749-111">Azure 부하 분산 장치 tooexpose 두 개의 프런트 엔드 IP 주소를 각 웹 사이트에 hello 웹 사이트에 대 한 toodistribute 트래픽 toohello 각 IP 구성에 대 한 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="75749-111">We use Azure Load Balancer tooexpose two frontend IP addresses, one for each website, toodistribute traffic toohello respective IP configuration for hello website.</span></span> <span data-ttu-id="75749-112">이 시나리오에서는으로 백 엔드 풀 IP 주소 모두 같은 포트 번호 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="75749-112">This scenario uses hello same port number across both frontends, as well as both backend pool IP addresses.</span></span>

![LB 시나리오 이미지](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a><span data-ttu-id="75749-114">여러 IP 구성에 대 한 단계 tooload 잔액</span><span class="sxs-lookup"><span data-stu-id="75749-114">Steps tooload balance on multiple IP configurations</span></span>

<span data-ttu-id="75749-115">이 문서에 설명 된 tooachieve hello 시나리오 아래 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="75749-115">Follow hello steps below tooachieve hello scenario outlined in this article:</span></span>

1. <span data-ttu-id="75749-116">Azure PowerShell을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="75749-116">Install Azure PowerShell.</span></span> <span data-ttu-id="75749-117">참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) hello 최신 버전의 Azure PowerShell을 설치, 구독을 선택 하 고 tooyour 계정에 로그인 하는 방법에 대 한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="75749-117">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for information about installing hello latest version of Azure PowerShell, selecting your subscription, and signing in tooyour account.</span></span>
2. <span data-ttu-id="75749-118">다음 설정을 hello를 사용 하 여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75749-118">Create a resource group using hello following settings:</span></span>

    ```powershell
    $location = "westcentralus".
    $myResourceGroup = "contosofabrikam"
    ```

    <span data-ttu-id="75749-119">자세한 내용은 [리소스 그룹 만들기](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)의 2단계를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75749-119">For more information, see Step 2 of [Create a Resource Group](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

3. <span data-ttu-id="75749-120">[가용성 집합 만들기](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json) toocontain Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="75749-120">[Create an Availability Set](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json) toocontain your VMs.</span></span> <span data-ttu-id="75749-121">이 시나리오에 대 한 hello 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="75749-121">For this scenario, use hello following command:</span></span>

    ```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset" -Location "West Central US"
    ```

4. <span data-ttu-id="75749-122">3-5에서 지침 단계에 따라 [Windows VM을 만들](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) 문서 tooprepare hello 단일 NIC 사용 하 여 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="75749-122">Follow instructions steps 3 through 5 in [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) article tooprepare hello creation of a VM with a single NIC.</span></span> <span data-ttu-id="75749-123">6.1, 단계를 실행 하 고 hello 다음 단계 6.2 대신 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="75749-123">Execute step 6.1, and use hello following instead of step 6.2:</span></span>

    ```powershell
    $availset = Get-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset"
    New-AzureRmVMConfig -VMName "VM1" -VMSize "Standard_DS1_v2" -AvailabilitySetId $availset.Id
    ```

    <span data-ttu-id="75749-124">그런 다음 [Windows VM 만들기](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)의 6.3 ~ 6.8단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="75749-124">Then complete [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) steps 6.3 through 6.8.</span></span>

5. <span data-ttu-id="75749-125">Hello Vm의 두 번째 IP 구성 tooeach를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="75749-125">Add a second IP configuration tooeach of hello VMs.</span></span> <span data-ttu-id="75749-126">Hello 지침에 따라 [toovirtual 컴퓨터에 여러 IP 주소 할당](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add) 문서.</span><span class="sxs-lookup"><span data-stu-id="75749-126">Follow hello instructions in [Assign multiple IP addresses toovirtual machines](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add) article.</span></span> <span data-ttu-id="75749-127">다음 구성 설정을 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="75749-127">Use hello following configuration settings:</span></span>

    ```powershell
    $NicName = "VM1-NIC2"
    $RgName = "contosofabrikam"
    $NicLocation = "West Central US"
    $IPConfigName4 = "VM1-ipconfig2"
    $Subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "mySubnet" -VirtualNetwork $myVnet
    ```

    <span data-ttu-id="75749-128">이 자습서의 hello 용도 대 한 공용 Ip와 tooassociate hello 보조 IP 구성 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="75749-128">You do not need tooassociate hello secondary IP configurations with public IPs for hello purpose of this tutorial.</span></span> <span data-ttu-id="75749-129">Hello 명령 tooremove hello 공개 IP 연결 부분을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="75749-129">Edit hello command tooremove hello public IP association part.</span></span>

6. <span data-ttu-id="75749-130">VM2에 대해 4 ~ 6단계를 다시 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="75749-130">Complete steps 4 through 6 of this article again for VM2.</span></span> <span data-ttu-id="75749-131">이렇게 할 때 있는지 tooreplace hello VM 이름 tooVM2 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75749-131">Be sure tooreplace hello VM name tooVM2 when doing this.</span></span> <span data-ttu-id="75749-132">Hello에 대 한 toocreate 가상 네트워크 필요 하지 않으면 VM의 두 번째입니다.</span><span class="sxs-lookup"><span data-stu-id="75749-132">Note that you do not need toocreate a virtual network for hello second VM.</span></span> <span data-ttu-id="75749-133">사용 사례를 기반으로 새 서브넷을 만들거나 만들지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75749-133">You may or may not create a new subnet based on your use case.</span></span>

7. <span data-ttu-id="75749-134">두 개의 공용 IP 주소를 만들고 표시 된 것 처럼 hello 적절 한 변수에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="75749-134">Create two public IP addresses and store them in hello appropriate variables as shown:</span></span>

    ```powershell
    $publicIP1 = New-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel contoso
    $publicIP2 = New-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel fabrikam

    $publicIP1 = Get-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam
    $publicIP2 = Get-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam
    ```

8. <span data-ttu-id="75749-135">두 개의 프런트 엔드 IP 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75749-135">Create two frontend IP configurations:</span></span>

    ```powershell
    $frontendIP1 = New-AzureRmLoadBalancerFrontendIpConfig -Name contosofe -PublicIpAddress $publicIP1
    $frontendIP2 = New-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2
    ```

9. <span data-ttu-id="75749-136">백 엔드 주소 풀, 프로브, 부하 분산 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75749-136">Create your backend address pools, a probe, and your load balancing rules:</span></span>

    ```powershell
    $beaddresspool1 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name contosopool
    $beaddresspool2 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool

    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HTTP -RequestPath 'index.html' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

    $lbrule1 = New-AzureRmLoadBalancerRuleConfig -Name HTTPc -FrontendIpConfiguration $frontendIP1 -BackendAddressPool $beaddresspool1 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    $lbrule2 = New-AzureRmLoadBalancerRuleConfig -Name HTTPf -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

10. <span data-ttu-id="75749-137">이러한 리소스를 만들었으면 부하 분산 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75749-137">Once you have these resources created, create your load balancer:</span></span>

    ```powershell
    $mylb = New-AzureRmLoadBalancer -ResourceGroupName contosofabrikam -Name mylb -Location 'West Central US' -FrontendIpConfiguration $frontendIP1 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

11. <span data-ttu-id="75749-138">Hello 두 번째 백 엔드 주소 풀 및 프런트 엔드 IP 구성 tooyour 새로 만든 부하 분산 장치를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="75749-138">Add hello second backend address pool and frontend IP configuration tooyour newly created load balancer:</span></span>

    ```powershell
    $mylb = Get-AzureRmLoadBalancer -Name "mylb" -ResourceGroupName $myResourceGroup | Add-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool | Set-AzureRmLoadBalancer

    $mylb | Add-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2 | Set-AzureRmLoadBalancer
    
    Add-AzureRmLoadBalancerRuleConfig -Name HTTP -LoadBalancer $mylb -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80 | Set-AzureRmLoadBalancer
    ```

12. <span data-ttu-id="75749-139">아래의 hello 명령 hello Nic를 가져오고 hello의 각 보조 NIC toohello 백 엔드 주소 풀의 IP 구성 모두 부하 분산 장치를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="75749-139">hello commands below get hello NICs and then add both IP configurations of each secondary NIC toohello backend address pool of hello load balancer:</span></span>

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

13. <span data-ttu-id="75749-140">마지막으로 DNS 리소스 레코드 toopoint toohello 각 프런트 엔드 IP 주소를 hello 부하 분산 장치를 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75749-140">Finally, you must configure DNS resource records toopoint toohello respective frontend IP address of hello Load Balancer.</span></span> <span data-ttu-id="75749-141">도메인을 Azure DNS에 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75749-141">You may host your domains in Azure DNS.</span></span> <span data-ttu-id="75749-142">Load Balancer와 Azure DNS를 사용하는 방법에 대한 자세한 내용은 [다른 Azure 서비스와 함께 Azure DNS 사용](../dns/dns-for-azure-services.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75749-142">For more information about using Azure DNS with Load Balancer, see [Using Azure DNS with other Azure services](../dns/dns-for-azure-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="75749-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="75749-143">Next steps</span></span>
- <span data-ttu-id="75749-144">에 Azure에서 서비스 toocombine 부하 분산 방법에 대 한 자세한 [부하 분산 서비스를 사용 하 여 Azure에서](../traffic-manager/traffic-manager-load-balancing-azure.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="75749-144">Learn more about how toocombine load balancing services in Azure in [Using load-balancing services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span></span>
- <span data-ttu-id="75749-145">다른 유형의 로그를 사용 하 여 Azure toomanage에 부하 분산 장치에 문제를 해결 하는 방법에 대해 알아봅니다 [Azure 부하 분산 장치에 대 한 로그 분석](../load-balancer/load-balancer-monitor-log.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="75749-145">Learn how you can use different types of logs in Azure toomanage and troubleshoot load balancer in [Log analytics for Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span></span>
