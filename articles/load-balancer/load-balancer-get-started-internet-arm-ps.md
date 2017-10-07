---
title: "aaaCreate Azure 인터넷 연결 부하 분산 장치-PowerShell | Microsoft Docs"
description: "어떻게 toocreate 인터넷 연결 부하 분산 장치 리소스 관리자의 PowerShell을 사용 하 여 알아봅니다"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 8257f548-7019-417f-b15f-d004a1eec826
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: e4e0e5271bc83c23fc62c0910e784c57d2b30065
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started"></a>PowerShell을 사용하여 Resource Manager에서 인터넷 연결 부하 분산 장치 만들기

> [!div class="op_single_selector"]
> * [포털](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [템플릿](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

이 문서에서는 hello 리소스 관리자 배포 모델에 설명 합니다. 수도 있습니다 [어떻게 toocreate 인터넷 연결 부하 분산 장치 hello 클래식 배포 모델을 사용 하 여 자세한](load-balancer-get-started-internet-classic-cli.md)합니다.

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-hello-solution-by-using-azure-powershell"></a>Azure PowerShell을 사용 하 여 hello 솔루션 배포

다음 절차를 수행 하는 hello toocreate 인터넷 연결 PowerShell과 함께 Azure 리소스 관리자를 사용 하 여 분산 장치를 로드 하는 방법을 설명 합니다. Azure 리소스 관리자와 각 리소스 만들어집니다 및 개별적으로 구성 된 한 다음 함께 toocreate 부하 분산 장치.

만들고 해야 개체 toodeploy 부하 분산 장치 뒤 hello 구성:

* 프런트 엔드 IP 구성: 들어오는 네트워크 트래픽에 대한 공용 IP(PIP) 주소를 포함합니다.
* 백 엔드 주소 풀: hello hello 부하 분산 장치에서 tooreceive 네트워크 트래픽을 가상 컴퓨터에 대 한 Nic (네트워크 인터페이스)를 포함 합니다.
* 부하 분산 규칙: hello 백 엔드 주소 풀의 hello 부하 분산 장치 tooa 포트에 공용 포트를 매핑하는 규칙을 포함 합니다.
* 인바운드 NAT 규칙: hello hello 백 엔드 주소 풀에서 특정 가상 컴퓨터에 대 한 부하 분산 장치 tooa 포트에 공용 포트를 매핑하는 규칙을 포함 합니다.
* 프로브: hello 백 엔드 주소 풀의 가상 컴퓨터 인스턴스 중 사용 된 검색 toocheck 가용성 상태를 포함합니다.

자세한 내용은 [부하 분산 장치에 대한 Azure Resource Manager 지원](load-balancer-arm.md)을 참조하세요.

## <a name="set-up-powershell-toouse-resource-manager"></a>PowerShell toouse 리소스 관리자 설정

PowerShell에 대 한 hello Azure 리소스 관리자 모듈의 최신 프로덕션 버전 hello 있는지 확인 합니다.

1. TooAzure에 로그인 합니다.

    ```powershell
    Login-AzureRmAccount
    ```

    메시지가 표시되면 자격 증명을 입력합니다.

2. Hello 계정에 대 한 hello 구독을 확인 합니다.

    ```powershell
    Get-AzureRmSubscription
    ```

3. Azure 구독 toouse 선택 합니다.

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. 리소스 그룹을 만듭니다. (기존 리소스 그룹을 사용하는 경우에는 이 단계를 건너뜁니다.)

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a>가상 네트워크 및 hello 프런트 엔드 IP 풀에 대 한 공용 IP 주소 만들기

1. 서브넷 및 가상 네트워크를 만듭니다.

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    New-AzureRmvirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. Azure 공용 IP 주소 리소스, 명명 된 만들기 **PublicIP**, hello DNS 이름 사용 하 여 프런트 엔드 IP 풀에서 사용 하는 toobe **loadbalancernrp.westus.cloudapp.azure.com**. 다음 명령을 hello hello를 사용 하 여 정적 할당 유형입니다.

    ```powershell
    $publicIP = New-AzureRmPublicIpAddress -Name PublicIp -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -DomainNameLabel loadbalancernrp
    ```

   > [!IMPORTANT]
   > hello 부하 분산 장치는 해당 FQDN에 대 한 접두사로 hello 공용 IP의 도메인 레이블을 hello를 사용합니다. 이 hello 부하 분산 장치 FQDN으로 hello 클라우드 서비스를 사용 하 여 hello 클래식 배포 모델에서 다릅니다.
   > 이 예제에서는 hello FQDN은 **loadbalancernrp.westus.cloudapp.azure.com**합니다.

## <a name="create-a-front-end-ip-pool-and-a-back-end-address-pool"></a>프런트 엔드 IP 풀 및 백 엔드 주소 풀 만들기

1. 명명 된 프런트 엔드 IP 풀 만들기 **LB 프런트 엔드** hello를 사용 하 여 **PublicIp** 리소스입니다.

    ```powershell
    $frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PublicIpAddress $publicIP
    ```

2. **LB-backend**라는 백 엔드 주소 풀을 만듭니다.

    ```powershell
    $beaddresspool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name LB-backend
    ```

## <a name="create-nat-rules-a-load-balancer-rule-a-probe-and-a-load-balancer"></a>NAT 규칙, 부하 분산 장치 규칙, 프로브 및 부하 분산 장치 만들기

이 예에서는 hello 다음 항목을 만듭니다.

* 3389 tooport 3441 포트에서 수신 되는 모든 트래픽을 NAT 규칙 tootranslate
* 3389 tooport 3442 포트에서 수신 되는 모든 트래픽을 NAT 규칙 tootranslate
* 명명 된 페이지에는 프로브 규칙 toocheck hello 상태 상태 **HealthProbe.aspx**
* 부하 분산 장치 규칙 toobalance hello에 포트 80 tooport 80에 들어오는 모든 트래픽을 hello 백 엔드 풀의 주소
* 이러한 개체를 모두 사용하는 부하 분산 장치

다음 단계를 사용:

1. Hello NAT 규칙을 만듭니다.

    ```powershell
    $inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP1 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

    $inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP2 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389
    ```

2. 상태 프로브를 만듭니다. 두 가지 방법으로 tooconfigure는 프로브

    HTTP 프로브

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    TCP 프로브

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

3. 부하 분산 장치를 만듭니다.

    ```powershell
    $lbrule = New-AzureRmLoadBalancerRuleConfig -Name HTTP -FrontendIpConfiguration $frontendIP -BackendAddressPool  $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

4. 이전에 만든 hello 개체를 사용 하 여 hello 부하 분산 장치를 만듭니다.

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name NRP-LB -Location 'West US' -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

## <a name="create-nics"></a>NIC 만들기

네트워크 인터페이스 만들기 (또는 기존 템플릿을 수정할) 다음 tooNAT 규칙, 부하 분산 장치 규칙 및 프로브 연결:

1. Hello Nic 만든 toobe 이곳 hello 가상 네트워크 및 가상 네트워크 서브넷 가져옵니다.

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. 명명 된 NIC를 만들고 **lb nic1 수**, 첫 번째 NAT 규칙 hello 및 hello 첫 번째 (및만) 백 엔드 주소 풀과 연결 합니다.

    ```powershell
    $backendnic1= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic1-be -Location 'West US' -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
    ```

3. 명명 된 NIC를 만들고 **lb nic2 수**, 두 번째 NAT 규칙의 hello 및 hello 첫 번째 (및만) 백 엔드 주소 풀과 연결 합니다.

    ```powershell
    $backendnic2= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic2-be -Location 'West US' -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
    ```

4. Hello Nic를 확인 합니다.

        $backendnic1

    예상 출력:

        Name                 : lb-nic1-be
        ResourceGroupName    : NRP-RG
        Location             : westus
        Id                   : /subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        Etag                 : W/"d448256a-e1df-413a-9103-a137e07276d1"
        ResourceGuid         : 896cac4f-152a-40b9-b079-3e2201a5906e
        ProvisioningState    : Succeeded
        Tags                 :
        VirtualMachine       : null
        IpConfigurations     : [
                            {
                            "Name": "ipconfig1",
                            "Etag": "W/\"d448256a-e1df-413a-9103-a137e07276d1\"",
                            "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/ipconfig1",
                            "PrivateIpAddress": "10.0.2.6",
                            "PrivateIpAllocationMethod": "Static",
                            "Subnet": {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/virtualNetworks/NRPVNet/subnets/LB-Subnet-BE"
                            },
                            "ProvisioningState": "Succeeded",
                            "PrivateIpAddressVersion": "IPv4",
                            "PublicIpAddress": {
                                "Id": null
                            },
                            "LoadBalancerBackendAddressPools": [
                                {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/backendAddressPools/LB-backend"
                                }
                            ],
                            "LoadBalancerInboundNatRules": [
                                {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/inboundNatRules/RDP1"
                                }
                            ],
                            "Primary": true,
                            "ApplicationGatewayBackendAddressPools": []
                            }
                        ]
        DnsSettings          : {
                            "DnsServers": [],
                            "AppliedDnsServers": [],
                            "InternalDomainNameSuffix": "prcwibzcuvie5hnxav0yjks2cd.dx.internal.cloudapp.net"
                        }
        EnableIPForwarding   : False
        NetworkSecurityGroup : null
        Primary              :

5. 사용 하 여 hello `Add-AzureRmVMNetworkInterface` cmdlet tooassign hello Nic toodifferent Vm입니다.

## <a name="create-a-virtual-machine"></a>가상 컴퓨터 만들기

가상 컴퓨터 만들기 및 NIC 할당에 대한 지침은 [PowerShell을 사용하여Azure VM 만들기](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)를 참조하세요.

## <a name="add-hello-network-interface-toohello-load-balancer"></a>Hello 네트워크 인터페이스 toohello 부하 분산 장치를 추가 합니다.

1. Azure에서 hello 부하 분산 장치를 검색 합니다.

    (아직 수행 하지 않은) 하는 경우 변수를 hello 부하 분산 장치 리소스를 로드 합니다. hello 변수 라고 **$lb**합니다. Hello 앞에서 만든 hello 부하 분산 장치 리소스에서 동일한 이름을 사용 합니다.

    ```powershell
    $lb= get-azurermloadbalancer -name NRP-LB -resourcegroupname NRP-RG
    ```

2. Hello 백 엔드로 구성 tooa 변수를 로드 합니다.

    ```powershell
    $backend=Get-AzureRmLoadBalancerBackendAddressPoolConfig -name LB-backend -LoadBalancer $lb
    ```

3. 변수를 이미 만든 hello 네트워크 인터페이스를 로드 합니다. 변수 이름이 hello **$nic**합니다. hello 네트워크 인터페이스 이름을 hello 동일한 hello에서 앞의 예입니다.

    ```powershell
    $nic =get-azurermnetworkinterface -name lb-nic1-be -resourcegroupname NRP-RG
    ```

4. Hello 네트워크 인터페이스에서 hello 백 엔드 구성을 변경 합니다.

    ```powershell
    $nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
    ```

5. Hello 네트워크 인터페이스 개체를 저장 합니다.

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```

    네트워크 인터페이스 toohello 부하 분산 장치 백 엔드 풀을 추가한 다음 해당 부하 분산 장치 리소스에 대 한 hello 부하 분산 규칙에 따라 네트워크 트래픽을 받기 시작 합니다.

## <a name="update-an-existing-load-balancer"></a>기존 부하 분산 장치 업데이트

1. Hello를 사용 하 여 부하를 분산 장치를 부하 분산 장치 개체 toohello 변수를 지정 하는 앞의 예제 hello **$slb** 를 사용 하 여 `Get-AzureLoadBalancer`합니다.

    ```powershell
    $slb = get-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
    ```

2. 다음 예제는 hello, hello 백 엔드 풀-tooan 기존 부하 분산 장치에 대 한 포트 81 hello 프런트 엔드 풀에서 및 8181 포트를 사용 하 여 인바운드 NAT 규칙-를 추가 합니다.

    ```powershell
    $slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol TCP
    ```

3. 사용 하 여 hello 새 구성을 저장 `Set-AzureLoadBalancer`합니다.

    ```powershell
    $slb | Set-AzureRmLoadBalancer
    ```

## <a name="remove-a-load-balancer"></a>부하 분산 장치 제거하기

Hello 명령을 사용 하 여 `Remove-AzureLoadBalancer` toodelete 명명 된 이전에 만든된 부하 분산 장치 **NRP LB** 리소스 그룹에 호출 **NRP RG**합니다.

```powershell
Remove-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
```

> [!NOTE]
> Hello 선택적 스위치를 사용 하면 **-Force** tooavoid hello 메시지 삭제를 표시 합니다.

## <a name="next-steps"></a>다음 단계

[내부 부하 분산 장치 구성 시작](load-balancer-get-started-ilb-arm-ps.md)

[부하 분산 장치 배포 모드 구성](load-balancer-distribution-mode.md)

[부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성](load-balancer-tcp-idle-timeout.md)
