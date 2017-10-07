---
title: "i p v 6-PowerShell aaaCreate Azure 인터넷 연결 부하 분산 장치 | Microsoft Docs"
description: "리소스 관리자에 대 한 PowerShell을 사용 하 여 i p v 6 분산 toocreate 인터넷 연결을 로드 하는 방법에 대해 알아봅니다"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
keywords: "ipv6, Azure Load Balancer, 이중 스택, 공용 IP, 기본 ipv6, 모바일, iot"
ms.assetid: d4c649e3-84ad-4343-8b6a-0e89f0b9e518
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 6ebb108399b070e06dddc33b7a774481eb44d717
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-with-ipv6-using-powershell-for-resource-manager"></a>PowerShell을 사용하여 리소스 관리자에 대한 IPv6를 포함한 인터넷 연결 부하 분산 장치 만들기 시작

> [!div class="op_single_selector"]
> * [PowerShell](load-balancer-ipv6-internet-ps.md)
> * [Azure CLI](load-balancer-ipv6-internet-cli.md)
> * [템플릿](load-balancer-ipv6-internet-template.md)

Azure 부하 분산 장치는 계층 4(TCP, UDP) 부하 분산 장치입니다. hello 부하 분산 장치 부하 분산 장치 집합의 가상 컴퓨터 또는 클라우드 서비스의 비정상 상태 서비스 인스턴스 간에 들어오는 트래픽을 분산 하 여 고가용성을 제공 합니다. Azure Load Balancer는 여러 포트, 여러 IP 주소 또는 둘 다에서 이러한 서비스를 제공할 수도 있습니다.

## <a name="example-deployment-scenario"></a>예제 배포 시나리오

hello 다음 다이어그램에서는 hello 부하 분산 되 고이 문서에 배포 된 솔루션입니다.

![부하 분산 장치 시나리오](./media/load-balancer-ipv6-internet-ps/lb-ipv6-scenario.png)

이 시나리오에서는 Azure 리소스를 수행 하는 hello를 만듭니다.

* IPv4 및 IPv6 공용 IP 주소를 가진 인터넷 연결 부하 분산 장치
* 두 개의 끝점을 로드 균형 조정 규칙 toomap hello 공용 Vip toohello 개인
* 가용성 집합 toothat hello 두 Vm이 포함
* 2개의 가상 컴퓨터(VM)
* 할당된 IPv4 및 IPv6 주소를 사용하는 각 VM에 대한 가상 네트워크 인터페이스

## <a name="deploying-hello-solution-using-hello-azure-powershell"></a>Hello Azure PowerShell을 사용 하 여 hello 솔루션 배포

단계를 수행 하는 hello toocreate 인터넷 연결 부하 분산 장치 Azure 리소스 관리자를 사용 하 여 PowerShell을 사용 하는 방법을 보여 줍니다. Azure 리소스 관리자와 각 리소스를 만들 고 toocreate 리소스는 조립 다음 개별적으로 구성 합니다.

부하 분산 장치 toodeploy 만들고 구성한 다음 개체는 hello:

* 프런트 엔드 IP 구성 - 들어오는 네트워크 트래픽에 대한 공용 IP 주소를 포함합니다.
* 백 엔드 주소 풀-hello hello 부하 분산 장치에서 가상 컴퓨터 tooreceive 네트워크 트래픽에 대 한 Nic (네트워크 인터페이스)를 포함 합니다.
* 부하 분산 규칙-hello 백 엔드 주소 풀의 부하 분산 장치 tooport hello에 공용 포트 매핑 규칙을 포함 합니다.
* 인바운드 NAT 규칙-hello hello 백 엔드 주소 풀에서 특정 가상 컴퓨터에 대 한 부하 분산 장치 tooa 포트에 공용 포트 매핑 규칙을 포함 합니다.
* 프로브-hello 백 엔드 주소 풀에 있는 가상 컴퓨터 인스턴스의 사용 된 검색 toocheck 가용성 상태를 포함 합니다.

자세한 내용은 [부하 분산 장치에 대한 Azure Resource Manager 지원](load-balancer-arm.md)을 참조하세요.

## <a name="set-up-powershell-toouse-resource-manager"></a>PowerShell toouse 리소스 관리자 설정

PowerShell에 대 한 hello Azure 리소스 관리자 모듈의 최신 프로덕션 버전 hello 있는지 확인 합니다.

1. Azure에 로그인

    ```powershell
    Login-AzureRmAccount
    ```

    메시지가 표시되면 자격 증명을 입력합니다.

2. Hello 계정에 대 한 hello 구독을 확인

    ```powershell
    Get-AzureRmSubscription
    ```

3. Azure 구독 toouse 선택 합니다.

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. 리소스 그룹을 만듭니다. 기존 리소스 그룹을 사용하는 경우에는 이 단계를 건너뛰세요.

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a>가상 네트워크 및 hello 프런트 엔드 IP 풀에 대 한 공용 IP 주소 만들기

1. 서브넷을 사용하는 가상 네트워크를 만듭니다.

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    $vnet = New-AzureRmvirtualNetwork -Name VNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. Azure 공용 IP 주소 hello 프런트 엔드 IP 주소 풀에 대 한 (PIP) 리소스를 만듭니다.

    ```powershell
    $publicIPv4 = New-AzureRmPublicIpAddress -Name 'pub-ipv4' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -IpAddressVersion IPv4 -DomainNameLabel lbnrpipv4
    $publicIPv6 = New-AzureRmPublicIpAddress -Name 'pub-ipv6' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Dynamic -IpAddressVersion IPv6 -DomainNameLabel lbnrpipv6
    ```

    > [!IMPORTANT]
    > hello 부하 분산 장치는 해당 FQDN에 대 한 접두사로 hello 공용 IP의 도메인 레이블을 hello를 사용합니다. 이 예제에서는 hello Fqdn은 *lbnrpipv4.westus.cloudapp.azure.com* 및 *lbnrpipv6.westus.cloudapp.azure.com*합니다.

## <a name="create-a-front-end-ip-configurations-and-a-back-end-address-pool"></a>프런트 엔드 IP 구성 및 백 엔드 주소 풀 만들기

1. 만든 hello 공용 IP 주소를 사용 하는 프런트 엔드 주소 구성을 만듭니다.

    ```powershell
    $FEIPConfigv4 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv4" -PublicIpAddress $publicIPv4
    $FEIPConfigv6 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv6" -PublicIpAddress $publicIPv6
    ```

2. 백 엔드 주소 풀을 만듭니다.

    ```powershell
    $backendpoolipv4 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv4"
    $backendpoolipv6 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv6"
    ```

## <a name="create-lb-rules-nat-rules-a-probe-and-a-load-balancer"></a>LB 규칙, NAT 규칙, 프로브 및 부하 분산 장치 만들기

이 예에서는 hello 다음 항목을 만듭니다.

* NAT 규칙 tootranslate 포트 443 tooport 4443에 들어오는 모든 트래픽을
* 부하 분산 장치 규칙 toobalance hello에 포트 80 tooport 80에 들어오는 모든 트래픽을 hello 백 엔드 풀에서 해결합니다.
* 부하 분산 장치 규칙 tooallow RDP 연결 toohello 포트 3389에 있는 Vm입니다.
* 명명 된 페이지에는 프로브 규칙 toocheck hello 상태 상태 *HealthProbe.aspx* 또는 포트 8080에서 서비스
* 이러한 개체를 모두 사용하는 부하 분산 장치

1. Hello NAT 규칙을 만듭니다.

    ```powershell
    $inboundNATRule1v4 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev4" -FrontendIpConfiguration $FEIPConfigv4 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    $inboundNATRule1v6 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev6" -FrontendIpConfiguration $FEIPConfigv6 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    ```

2. 상태 프로브를 만듭니다. 두 가지 방법으로 tooconfigure는 프로브

    HTTP 프로브

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    또는 TCP 프로브

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -Protocol Tcp -Port 8080 -IntervalInSeconds 15 -ProbeCount 2
    $RDPprobe = New-AzureRmLoadBalancerProbeConfig -Name 'RDPprobe' -Protocol Tcp -Port 3389 -IntervalInSeconds 15 -ProbeCount 2
    ```

    이 예에서는 TCP 프로브 toouse hello를 하겠습니다.

3. 부하 분산 장치를 만듭니다.

    ```powershell
    $lbrule1v4 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv4" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $lbrule1v6 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv6" -FrontendIpConfiguration $FEIPConfigv6 -BackendAddressPool $backendpoolipv6 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $RDPrule = New-AzureRmLoadBalancerRuleConfig -Name "RDPrule" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $RDPprobe -Protocol Tcp -FrontendPort 3389 -BackendPort 3389
    ```

4. 이전에 만든 hello 개체를 사용 하 여 hello 부하 분산 장치를 만듭니다.

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name 'myNrpIPv6LB' -Location 'West US' -FrontendIpConfiguration $FEIPConfigv4,$FEIPConfigv6 -InboundNatRule $inboundNATRule1v6,$inboundNATRule1v4 -BackendAddressPool $backendpoolipv4,$backendpoolipv6 -Probe $healthProbe,$RDPprobe -LoadBalancingRule $lbrule1v4,$lbrule1v6,$RDPrule
    ```

## <a name="create-nics-for-hello-back-end-vms"></a>백 엔드 Vm hello에 대 한 Nic를 만들려면

1. 가져오기 hello 가상 네트워크 및 가상 네트워크 서브넷의 Nic hello 이곳 toobe 생성 합니다.

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name VNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. Hello Vm에 대 한 IP 구성 및 Nic를 만듭니다.

    ```powershell
    $nic1IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4 -LoadBalancerInboundNatRule $inboundNATRule1v4
    $nic1IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6 -LoadBalancerInboundNatRule $inboundNATRule1v6
    $nic1 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic0' -IpConfiguration $nic1IPv4,$nic1IPv6 -ResourceGroupName NRP-RG -Location 'West US'

    $nic2IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4
    $nic2IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6
    $nic2 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic1' -IpConfiguration $nic2IPv4,$nic2IPv6 -ResourceGroupName NRP-RG -Location 'West US'
    ```

## <a name="create-virtual-machines-and-assign-hello-newly-created-nics"></a>가상 컴퓨터를 만들고 새로 만든 Nic hello를 할당

VM 만들기에 대한 자세한 내용은 [리소스 관리자 및 Azure PowerShell을 사용하여 Windows 가상 컴퓨터 만들기 및 미리 구성](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)

1. 가용성 집합 및 저장소 계정 만들기

    ```powershell
    New-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG -location 'West US'
    $availabilitySet = Get-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG
    New-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct' -Location 'West US' -SkuName "Standard_LRS"
    $CreatedStorageAccount = Get-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct'
    ```

2. 각 VM을 만들고 만든 hello 이전 Nic를 할당 합니다.

    ```powershell
    $mySecureCredentials= Get-Credential -Message "Type hello username and password of hello local administrator account."

    $vm1 = New-AzureRmVMConfig -VMName 'myNrpIPv6VM0' -VMSize 'Standard_G1' -AvailabilitySetId $availabilitySet.Id
    $vm1 = Set-AzureRmVMOperatingSystem -VM $vm1 -Windows -ComputerName 'myNrpIPv6VM0' -Credential $mySecureCredentials -ProvisionVMAgent -EnableAutoUpdate
    $vm1 = Set-AzureRmVMSourceImage -VM $vm1 -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm1 = Add-AzureRmVMNetworkInterface -VM $vm1 -Id $nic1.Id -Primary
    $osDisk1Uri = $CreatedStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/myNrpIPv6VM0osdisk.vhd"
    $vm1 = Set-AzureRmVMOSDisk -VM $vm1 -Name 'myNrpIPv6VM0osdisk' -VhdUri $osDisk1Uri -CreateOption FromImage
    New-AzureRmVM -ResourceGroupName NRP-RG -Location 'West US' -VM $vm1

    $vm2 = New-AzureRmVMConfig -VMName 'myNrpIPv6VM1' -VMSize 'Standard_G1' -AvailabilitySetId $availabilitySet.Id
    $vm2 = Set-AzureRmVMOperatingSystem -VM $vm2 -Windows -ComputerName 'myNrpIPv6VM1' -Credential $mySecureCredentials -ProvisionVMAgent -EnableAutoUpdate
    $vm2 = Set-AzureRmVMSourceImage -VM $vm2 -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm2 = Add-AzureRmVMNetworkInterface -VM $vm2 -Id $nic2.Id -Primary
    $osDisk2Uri = $CreatedStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/myNrpIPv6VM1osdisk.vhd"
    $vm2 = Set-AzureRmVMOSDisk -VM $vm2 -Name 'myNrpIPv6VM1osdisk' -VhdUri $osDisk2Uri -CreateOption FromImage
    New-AzureRmVM -ResourceGroupName NRP-RG -Location 'West US' -VM $vm2
    ```

## <a name="next-steps"></a>다음 단계

[내부 부하 분산 장치 구성 시작](load-balancer-get-started-ilb-arm-ps.md)

[부하 분산 장치 배포 모드 구성](load-balancer-distribution-mode.md)

[부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성](load-balancer-tcp-idle-timeout.md)
