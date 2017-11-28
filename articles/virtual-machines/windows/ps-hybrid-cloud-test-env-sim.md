---
title: "시뮬레이션된 하이브리드 클라우드 테스트 환경 | Microsoft Docs"
description: "Azure 가상 네트워크 두 개와 VNet 간 연결을 사용하여 IT 전문가 또는 개발 테스트용 시뮬레이션된 하이브리드 클라우드 환경을 만들어봅니다."
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ca5bf294-8172-44a9-8fed-d6f38d345364
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.openlocfilehash: 4ec6f079b762a25894d822bfc098ea5442a1f7e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-a-simulated-hybrid-cloud-environment-for-testing"></a><span data-ttu-id="f7a93-103">테스트용 시뮬레이션된 하이브리드 클라우드 환경 설정</span><span class="sxs-lookup"><span data-stu-id="f7a93-103">Set up a simulated hybrid cloud environment for testing</span></span>
<span data-ttu-id="f7a93-104">이 문서에서는 두 개의 Azure 가상 네트워크를 사용하여 Microsoft Azure에서 시뮬레이션된 하이브리드 클라우드 환경을 만드는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-104">This article steps you through creating a simulated hybrid cloud environment with Microsoft Azure using two Azure virtual networks.</span></span> <span data-ttu-id="f7a93-105">다음은 결과 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-105">Here is the resulting configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

<span data-ttu-id="f7a93-106">하이브리드 클라우드 프로덕션 환경을 시뮬레이션하고 다음으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-106">This simulates a hybrid cloud production environment and consists of:</span></span>

* <span data-ttu-id="f7a93-107">Azure 가상 네트워크(TestLab 가상 네트워크)에서 호스트되는 시뮬레이션 및 간소화된 온-프레미스 네트워크</span><span class="sxs-lookup"><span data-stu-id="f7a93-107">A simulated and simplified on-premises network hosted in an Azure virtual network (the TestLab virtual network).</span></span>
* <span data-ttu-id="f7a93-108">Azure에서 호스트되는 시뮬레이션된 크로스-프레미스 가상 네트워크(TestVNET)</span><span class="sxs-lookup"><span data-stu-id="f7a93-108">A simulated cross-premises virtual network hosted in Azure (TestVNET).</span></span>
* <span data-ttu-id="f7a93-109">두 가상 네트워크의 VNet 간 연결</span><span class="sxs-lookup"><span data-stu-id="f7a93-109">A VNet-to-VNet connection between the two virtual networks.</span></span>
* <span data-ttu-id="f7a93-110">TestVNET 가상 네트워크의 보조 도메인 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="f7a93-110">A secondary domain controller in the TestVNET virtual network.</span></span>

<span data-ttu-id="f7a93-111">이 구성은 다음 작업을 수행할 수 있는 기초 및 일반적인 시작 지점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-111">This provides a basis and common starting point from which you can:</span></span>

* <span data-ttu-id="f7a93-112">시뮬레이션된 하이브리드 클라우드 환경에서 응용 프로그램 개발 및 테스트</span><span class="sxs-lookup"><span data-stu-id="f7a93-112">Develop and test applications in a simulated hybrid cloud environment.</span></span>
* <span data-ttu-id="f7a93-113">일부는 TestLab 가상 네트워크 내에 있고 일부는 TestVNET 가상 네트워크에 있는 컴퓨터의 테스트 구성을 만들어 하이브리드 클라우드 기반 IT 작업을 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-113">Create test configurations of computers, some within the TestLab virtual network and some within the TestVNET virtual network, to simulate hybrid cloud-based IT workloads.</span></span>

<span data-ttu-id="f7a93-114">이 하이브리드 클라우드 테스트 환경을 설정하는 네 가지 주요 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-114">There are four major phases to setting up this hybrid cloud test environment:</span></span>

1. <span data-ttu-id="f7a93-115">TestLab 가상 네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="f7a93-115">Configure the TestLab virtual network.</span></span>
2. <span data-ttu-id="f7a93-116">크로스-프레미스 가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="f7a93-116">Create the cross-premises virtual network.</span></span>
3. <span data-ttu-id="f7a93-117">VNet 간 VPN 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="f7a93-117">Create the VNet-to-VNet VPN connection.</span></span>
4. <span data-ttu-id="f7a93-118">DC2 구성</span><span class="sxs-lookup"><span data-stu-id="f7a93-118">Configure DC2.</span></span> 

<span data-ttu-id="f7a93-119">이 구성에는 Azure 구독이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-119">This configuration requires an Azure subscription.</span></span> <span data-ttu-id="f7a93-120">MSDN 또는 Visual Studio 구독이 있는 경우에는 [Visual Studio 구독자를 위한 월간 Azure 크레딧](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7a93-120">If you have an MSDN or Visual Studio subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span>

> [!NOTE]
> <span data-ttu-id="f7a93-121">Azure의 가상 컴퓨터 및 가상 네트워크 게이트웨이는 실행 중인 동안 지속적인 비용이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-121">Virtual machines and virtual network gateways in Azure incur an ongoing monetary cost when they are running.</span></span> <span data-ttu-id="f7a93-122">이 비용은 MSDN 또는 유료 구독에 대해 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-122">This cost is billed against your MSDN or paid subscription.</span></span> <span data-ttu-id="f7a93-123">Azure VPN 게이트웨이는 두 개의 Azure 가상 컴퓨터 집합으로 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-123">An Azure VPN gateway is implemented as a set of two Azure virtual machines.</span></span> <span data-ttu-id="f7a93-124">비용을 최소화하려면 테스트 환경을 만들고 가능한 한 신속하게 필요한 테스트 및 데모를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-124">To minimize the costs, create the test environment and perform your needed testing and demonstration as quickly as possible.</span></span>
> 
> 

## <a name="phase-1-configure-the-testlab-virtual-network"></a><span data-ttu-id="f7a93-125">1단계: TestLab 가상 네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="f7a93-125">Phase 1: Configure the TestLab virtual network</span></span>
<span data-ttu-id="f7a93-126">[기본 구성 테스트 환경](https://technet.microsoft.com/library/mt771177.aspx) 항목에 설명된 지침을 사용하여 TestLab이라는 Azure 가상 네트워크에서 DC1, APP1 및 CLIENT1 컴퓨터를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-126">Use the instructions in the [Base Configuration test environment](https://technet.microsoft.com/library/mt771177.aspx) topic to configure the DC1, APP1, and CLIENT1 computers in the Azure virtual network named TestLab.</span></span> 

<span data-ttu-id="f7a93-127">다음으로 Azure PowerShell 프롬프트를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-127">Next, start an Azure PowerShell prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="f7a93-128">다음 명령 집합은 Azure PowerShell 1.0 이상을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-128">The following command sets use Azure PowerShell 1.0 and later.</span></span>
> 
> 

<span data-ttu-id="f7a93-129">계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-129">Sign in to your account.</span></span>

    Login-AzureRMAccount

<span data-ttu-id="f7a93-130">다음 명령을 사용하여 구독 이름을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-130">Get your subscription name using the following command.</span></span>

    Get-AzureRMSubscription | Sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="f7a93-131">Azure 구독을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-131">Set your Azure subscription.</span></span> <span data-ttu-id="f7a93-132">1단계에서 기본 구성을 빌드하는 데 사용했던 동일한 구독을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-132">Use the same subscription that you used to build your base configuration in Phase 1.</span></span> <span data-ttu-id="f7a93-133">< 및 > 문자를 포함하여 따옴표 안의 모든 항목을 올바른 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-133">Replace everything within the quotes, including the < and > characters, with the correct name.</span></span>

    $subscr="<subscription name>"
    Get-AzureRmSubscription –SubscriptionName $subscr | Select-AzureRmSubscription

<span data-ttu-id="f7a93-134">그런 다음 Azure 게이트웨이를 호스트하는 데 사용할 기본 구성의 TestLab 가상 네트워크에 게이트웨이 서브넷을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-134">Next, add a gateway subnet to the TestLab virtual network of your base configuration, which will be used to host the Azure gateway.</span></span>

    $rgName="<name of your resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed the TestLab virtual network, such as West US>"
    $vnet=Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name TestLab
    Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 10.255.255.248/29 -VirtualNetwork $vnet
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet

<span data-ttu-id="f7a93-135">그런 다음 TestLab 가상 네트워크의 게이트웨이에 할당할 공용 IP 주소를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-135">Next, request a public IP address to assign to the gateway for the TestLab virtual network.</span></span>

    $gwpip=New-AzureRmPublicIpAddress -Name TestLab_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic

<span data-ttu-id="f7a93-136">그런 다음 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-136">Next, create your gateway.</span></span>

    $vnet=Get-AzureRmVirtualNetwork -Name TestLab -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name TestLab_GWConfig -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id 
    New-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

<span data-ttu-id="f7a93-137">새 게이트웨이를 만드는 데 20분 이상 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-137">Keep in mind that new gateways can take 20 minutes or more to create.</span></span>

<span data-ttu-id="f7a93-138">로컬 컴퓨터의 Azure 포털에서 CORP\User1 자격 증명을 사용하여 DC1에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-138">From the Azure portal on your local computer, connect to DC1 with the CORP\User1 credentials.</span></span> <span data-ttu-id="f7a93-139">컴퓨터 및 사용자가 해당 로컬 도메인 컨트롤러를 사용하여 인증할 수 있도록 CORP 도메인을 구성하려면 DC1에서 관리자 수준 Windows PowerShell 명령 프롬프트의 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-139">To configure the CORP domain so that computers and users use their local domain controller for authentication, run these commands from an administrator-level Windows PowerShell command prompt on DC1.</span></span>

    New-ADReplicationSite -Name "TestLab" 
    New-ADReplicationSite -Name "TestVNET"
    New-ADReplicationSubnet -Name "10.0.0.0/8" -Site "TestLab"
    New-ADReplicationSubnet -Name "192.168.0.0/16" -Site "TestVNET"

<span data-ttu-id="f7a93-140">다음은 현재 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-140">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph1.png)

## <a name="phase-2-create-the-testvnet-virtual-network"></a><span data-ttu-id="f7a93-141">2단계: TestVNET 가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="f7a93-141">Phase 2: Create the TestVNET virtual network</span></span>
<span data-ttu-id="f7a93-142">먼저 TestVNET 가상 네트워크를 만들고 네트워크 보안 그룹으로 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-142">First, create the TestVNET virtual network and protect it with a network security group.</span></span>

    $rgName="<name of the resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed the TestLab virtual network, such as West US>"
    $locShortName="<Azure location name from $locName in all lowercase letters with spaces removed. Example:  westus>"
    $testSubnet=New-AzureRMVirtualNetworkSubnetConfig -Name "TestSubnet" -AddressPrefix 192.168.0.0/24
    $gatewaySubnet=New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 192.168.255.248/29
    New-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName -Location $locName -AddressPrefix 192.168.0.0/16 -Subnet $testSubnet,$gatewaySubnet –DNSServer 10.0.0.4
    $rule1=New-AzureRMNetworkSecurityRuleConfig -Name "RDPTraffic" -Description "Allow RDP to all VMs on the subnet" -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * -DestinationPortRange 3389
    New-AzureRMNetworkSecurityGroup -Name "TestSubnet" -ResourceGroupName $rgName -Location $locShortName -SecurityRules $rule1
    $vnet=Get-AzureRMVirtualNetwork -ResourceGroupName $rgName -Name TestVNET
    $nsg=Get-AzureRMNetworkSecurityGroup -Name "TestSubnet" -ResourceGroupName $rgName
    Set-AzureRMVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet" -AddressPrefix 192.168.0.0/24 -NetworkSecurityGroup $nsg

<span data-ttu-id="f7a93-143">그런 다음 TestVNET 가상 네트워크의 게이트웨이에 할당할 공용 IP 주소를 요청하고 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-143">Next, request a public IP address to be allocated to the gateway for the TestVNET virtual network and create your gateway.</span></span>

    $gwpip=New-AzureRmPublicIpAddress -Name TestVNET_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $vnet=Get-AzureRmVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name "TestVNET_GWConfig" -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
    New-AzureRmVirtualNetworkGateway -Name "TestVNET_GW" -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

<span data-ttu-id="f7a93-144">다음은 현재 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-144">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph2.png)

## <a name="phase-3-create-the-vnet-to-vnet-connection"></a><span data-ttu-id="f7a93-145">3단계: VNet 간 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="f7a93-145">Phase 3: Create the VNet-to-VNet connection</span></span>
<span data-ttu-id="f7a93-146">먼저 네트워크 또는 보안 관리자에서 임의로 암호화된 강력한 32자의 미리 공유한 키를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-146">First, obtain a random, cryptographically strong, 32-character pre-shared key from your network or security administrator.</span></span> <span data-ttu-id="f7a93-147">또는 [IPsec 미리 공유한 키에 대한 임의 문자열 만들기](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx) 에서 정보를 사용하여 미리 공유한 키를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-147">Alternately, use the information at [Create a random string for an IPsec preshared key](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx) to obtain a pre-shared key.</span></span>

<span data-ttu-id="f7a93-148">그리고 나서 다음 명령을 사용하여 VNet 간 VPN 연결을 만듭니다. 이를 완료하려면 다소 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-148">Next, use these commands to create the VNet-to-VNet VPN connection, which can take some time to complete.</span></span>

    $sharedKey="<pre-shared key value>"
    $gwTestLab=Get-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName
    $gwTestVNET=Get-AzureRmVirtualNetworkGateway -Name TestVNET_GW -ResourceGroupName $rgName
    New-AzureRmVirtualNetworkGatewayConnection -Name TestLab_to_TestVNET -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestLab -VirtualNetworkGateway2 $gwTestVNET -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey
    New-AzureRmVirtualNetworkGatewayConnection -Name TestVNET_to_TestLab -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestVNET -VirtualNetworkGateway2 $gwTestLab -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey

<span data-ttu-id="f7a93-149">잠시 후에 연결이 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-149">After a few minutes, the connection should be established.</span></span>

<span data-ttu-id="f7a93-150">다음은 현재 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-150">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph3.png)

## <a name="phase-4-configure-dc2"></a><span data-ttu-id="f7a93-151">4단계: DC2 구성</span><span class="sxs-lookup"><span data-stu-id="f7a93-151">Phase 4: Configure DC2</span></span>
<span data-ttu-id="f7a93-152">먼저 DC2에 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-152">First, create a virtual machine for DC2.</span></span> <span data-ttu-id="f7a93-153">로컬 컴퓨터의 Azure PowerShell 명령 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-153">Run these commands at the Azure PowerShell command prompt on your local computer.</span></span>

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<the storage account name for the base configuration>"
    $vnet=Get-AzureRMVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $pip=New-AzureRMPublicIpAddress -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -PrivateIpAddress 192.168.0.4
    $vm=New-AzureRMVMConfig -VMName DC2 -VMSize Standard_A1
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/DC2-TestVNET-ADDSDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name ADDS-Data -DiskSizeInGB 20 -VhdUri $vhdURI  -CreateOption empty
    $cred=Get-Credential -Message "Type the name and password of the local administrator account for DC2."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName DC2 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/DC2-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name DC2-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="f7a93-154">다음으로 Azure 포털에서 새 DC2 가상 컴퓨터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-154">Next, connect to the new DC2 virtual machine from the Azure portal.</span></span>

<span data-ttu-id="f7a93-155">그런 다음 기본 연결 테스트에 대한 트래픽을 허용하도록 Windows 방화벽 규칙을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-155">Next, configure a Windows Firewall rule to allow traffic for basic connectivity testing.</span></span> <span data-ttu-id="f7a93-156">DC2의 관리자 수준 Windows PowerShell 명령 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-156">From an administrator-level Windows PowerShell command prompt on DC2, run these commands.</span></span>

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc1.corp.contoso.com

<span data-ttu-id="f7a93-157">Ping 명령을 실행한 경우 IP 주소 10.0.0.4에서 성공적인 회신 4개가 수신되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-157">The ping command should result in four successful replies from IP address 10.0.0.4.</span></span> <span data-ttu-id="f7a93-158">이는 VNet 간 연결의 트래픽에 대한 테스트입니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-158">This is a test of traffic across the VNet-to-VNet connection.</span></span>

<span data-ttu-id="f7a93-159">다음으로 DC2에서 추가 데이터 디스크를 드라이브 문자가 F:인 새 볼륨으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-159">Next, add the extra data disk on DC2 as a new volume with the drive letter F:.</span></span>

1. <span data-ttu-id="f7a93-160">Server Manager의 왼쪽 창에서 **파일 및 저장소 서비스**를 클릭한 다음 **디스크**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-160">In the left pane of Server Manager, click **File and Storage Services**, and then click **Disks**.</span></span>
2. <span data-ttu-id="f7a93-161">내용 창의 **디스크** 그룹에서 **디스크 2**(**파티션**이 **알 수 없음**으로 설정됨)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-161">In the contents pane, in the **Disks** group, click **disk 2** (with the **Partition** set to **Unknown**).</span></span>
3. <span data-ttu-id="f7a93-162">**작업**을 클릭한 후 **새 볼륨**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-162">Click **Tasks**, and then click **New Volume**.</span></span>
4. <span data-ttu-id="f7a93-163">새 볼륨 마법사의 시작하기 전에 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-163">On the Before you begin page of the New Volume Wizard, click **Next**.</span></span>
5. <span data-ttu-id="f7a93-164">서버 및 디스크 선택 페이지에서 **디스크 2**를 클릭하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-164">On the Select the server and disk page, click **Disk 2**, and then click **Next**.</span></span> <span data-ttu-id="f7a93-165">메시지가 표시되면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-165">When prompted, click **OK**.</span></span>
6. <span data-ttu-id="f7a93-166">볼륨 크기를 선택합니다 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-166">On the Specify the size of the volume page, click **Next**.</span></span>
7. <span data-ttu-id="f7a93-167">드라이브 문자 또는 폴더에 할당 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-167">On the Assign to a drive letter or folder page, click **Next**.</span></span>
8. <span data-ttu-id="f7a93-168">파일 시스템 설정 선택 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-168">On the Select file system settings page, click **Next**.</span></span>
9. <span data-ttu-id="f7a93-169">선택 확인 페이지에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-169">On the Confirm selections page, click **Create**.</span></span>
10. <span data-ttu-id="f7a93-170">완료되면 **닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-170">When complete, click **Close**.</span></span>

<span data-ttu-id="f7a93-171">그런 다음 DC2를 corp.contoso.com 도메인의 복제본 도메인 컨트롤러로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-171">Next, configure DC2 as a replica domain controller for the corp.contoso.com domain.</span></span> <span data-ttu-id="f7a93-172">DC2의 관리자 수준 Windows PowerShell 명령 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-172">Run these commands from the Windows PowerShell command prompt on DC2.</span></span>

    Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
    Install-ADDSDomainController -Credential (Get-Credential CORP\User1) -DomainName "corp.contoso.com" -InstallDns:$true -DatabasePath "F:\NTDS" -LogPath "F:\Logs" -SysvolPath "F:\SYSVOL"

<span data-ttu-id="f7a93-173">CORP\User1 암호와 DSRM(디렉터리 서비스 복원 모드) 암호를 둘 다 제공하고 DC2를 다시 시작하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-173">Note that you are prompted to supply both the CORP\User1 password and a Directory Services Restore Mode (DSRM) password, and to restart DC2.</span></span>

<span data-ttu-id="f7a93-174">TestVNET 가상 네트워크에는 고유한 DNS 서버(DC2)가 있으므로 이 DNS 서버를 사용하도록 TestVNET 가상 네트워크를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-174">Now that the TestVNET virtual network has its own DNS server (DC2), you must configure the TestVNET virtual network to use this DNS server.</span></span>

1. <span data-ttu-id="f7a93-175">Azure 포털의 왼쪽 창에서 가상 네트워크 아이콘을 클릭한 다음 **TestVNET**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-175">In the left pane of the Azure portal, click the virtual networks icon, and then click **TestVNET**.</span></span>
2. <span data-ttu-id="f7a93-176">**설정** 탭에서 **DNS 서버**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-176">On the **Settings** tab, click **DNS servers**.</span></span>
3. <span data-ttu-id="f7a93-177">**주 DNS 서버**에서 10.0.0.4를 **192.168.0.4**로 바꿔 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-177">In **Primary DNS server**, type **192.168.0.4** to replace 10.0.0.4.</span></span>
4. <span data-ttu-id="f7a93-178">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-178">Click **Save**.</span></span>

<span data-ttu-id="f7a93-179">다음은 현재 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-179">This is your current configuration.</span></span> 

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

<span data-ttu-id="f7a93-180">이제 시뮬레이션된 하이브리드 클라우드 환경을 테스트할 준비가 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-180">Your simulated hybrid cloud environment is now ready for testing.</span></span>

## <a name="next-step"></a><span data-ttu-id="f7a93-181">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f7a93-181">Next step</span></span>
* <span data-ttu-id="f7a93-182">이 환경에서 [웹 기반 LOB(기간 업무) 응용 프로그램](ps-hybrid-cloud-test-env-lob.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f7a93-182">Set up a [web-based, line of business application](ps-hybrid-cloud-test-env-lob.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in this environment.</span></span>

