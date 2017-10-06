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
# <a name="load-balancing-on-multiple-ip-configurations-using-powershell"></a>PowerShell을 사용하여 여러 IP 구성의 부하 분산

> [!div class="op_single_selector"]
> * [포털](load-balancer-multiple-ip.md)
> * [CLI](load-balancer-multiple-ip-cli.md)
> * [PowerShell](load-balancer-multiple-ip-powershell.md)

이 문서에서는 Azure 부하 분산 장치에서 여러 ip toouse 보조 네트워크 인터페이스 (NIC)에서 해결 하는 방법을 설명 합니다. 이 시나리오에는 Windows를 실행하는 VM이 둘 있고 각각 기본 및 보조 NIC가 있습니다. 각 보조 hello Nic가 두 개의 IP 구성 합니다. 각 VM은 contoso.com 및 fabrikam.com 웹 사이트를 둘 다 호스트합니다. 각 웹 사이트는 hello 보조 NIC에서 hello IP 구성의 바인딩된 tooone Azure 부하 분산 장치 tooexpose 두 개의 프런트 엔드 IP 주소를 각 웹 사이트에 hello 웹 사이트에 대 한 toodistribute 트래픽 toohello 각 IP 구성에 대 한 사용 합니다. 이 시나리오에서는으로 백 엔드 풀 IP 주소 모두 같은 포트 번호 hello 합니다.

![LB 시나리오 이미지](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a>여러 IP 구성에 대 한 단계 tooload 잔액

이 문서에 설명 된 tooachieve hello 시나리오 아래 hello 단계를 수행 합니다.

1. Azure PowerShell을 설치합니다. 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) hello 최신 버전의 Azure PowerShell을 설치, 구독을 선택 하 고 tooyour 계정에 로그인 하는 방법에 대 한 정보에 대 한 합니다.
2. 다음 설정을 hello를 사용 하 여 리소스 그룹을 만듭니다.

    ```powershell
    $location = "westcentralus".
    $myResourceGroup = "contosofabrikam"
    ```

    자세한 내용은 [리소스 그룹 만들기](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)의 2단계를 참조하세요.

3. [가용성 집합 만들기](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json) toocontain Vm입니다. 이 시나리오에 대 한 hello 다음 명령을 사용 합니다.

    ```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset" -Location "West Central US"
    ```

4. 3-5에서 지침 단계에 따라 [Windows VM을 만들](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) 문서 tooprepare hello 단일 NIC 사용 하 여 VM 만들기 6.1, 단계를 실행 하 고 hello 다음 단계 6.2 대신 사용 합니다.

    ```powershell
    $availset = Get-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset"
    New-AzureRmVMConfig -VMName "VM1" -VMSize "Standard_DS1_v2" -AvailabilitySetId $availset.Id
    ```

    그런 다음 [Windows VM 만들기](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)의 6.3 ~ 6.8단계를 완료합니다.

5. Hello Vm의 두 번째 IP 구성 tooeach를 추가 합니다. Hello 지침에 따라 [toovirtual 컴퓨터에 여러 IP 주소 할당](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add) 문서. 다음 구성 설정을 hello를 사용 합니다.

    ```powershell
    $NicName = "VM1-NIC2"
    $RgName = "contosofabrikam"
    $NicLocation = "West Central US"
    $IPConfigName4 = "VM1-ipconfig2"
    $Subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "mySubnet" -VirtualNetwork $myVnet
    ```

    이 자습서의 hello 용도 대 한 공용 Ip와 tooassociate hello 보조 IP 구성 필요가 없습니다. Hello 명령 tooremove hello 공개 IP 연결 부분을 편집 합니다.

6. VM2에 대해 4 ~ 6단계를 다시 완료합니다. 이렇게 할 때 있는지 tooreplace hello VM 이름 tooVM2 수 있습니다. Hello에 대 한 toocreate 가상 네트워크 필요 하지 않으면 VM의 두 번째입니다. 사용 사례를 기반으로 새 서브넷을 만들거나 만들지 않을 수 있습니다.

7. 두 개의 공용 IP 주소를 만들고 표시 된 것 처럼 hello 적절 한 변수에 저장 합니다.

    ```powershell
    $publicIP1 = New-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel contoso
    $publicIP2 = New-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel fabrikam

    $publicIP1 = Get-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam
    $publicIP2 = Get-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam
    ```

8. 두 개의 프런트 엔드 IP 구성을 만듭니다.

    ```powershell
    $frontendIP1 = New-AzureRmLoadBalancerFrontendIpConfig -Name contosofe -PublicIpAddress $publicIP1
    $frontendIP2 = New-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2
    ```

9. 백 엔드 주소 풀, 프로브, 부하 분산 규칙을 만듭니다.

    ```powershell
    $beaddresspool1 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name contosopool
    $beaddresspool2 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool

    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HTTP -RequestPath 'index.html' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

    $lbrule1 = New-AzureRmLoadBalancerRuleConfig -Name HTTPc -FrontendIpConfiguration $frontendIP1 -BackendAddressPool $beaddresspool1 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    $lbrule2 = New-AzureRmLoadBalancerRuleConfig -Name HTTPf -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

10. 이러한 리소스를 만들었으면 부하 분산 장치를 만듭니다.

    ```powershell
    $mylb = New-AzureRmLoadBalancer -ResourceGroupName contosofabrikam -Name mylb -Location 'West Central US' -FrontendIpConfiguration $frontendIP1 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

11. Hello 두 번째 백 엔드 주소 풀 및 프런트 엔드 IP 구성 tooyour 새로 만든 부하 분산 장치를 추가 합니다.

    ```powershell
    $mylb = Get-AzureRmLoadBalancer -Name "mylb" -ResourceGroupName $myResourceGroup | Add-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool | Set-AzureRmLoadBalancer

    $mylb | Add-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2 | Set-AzureRmLoadBalancer
    
    Add-AzureRmLoadBalancerRuleConfig -Name HTTP -LoadBalancer $mylb -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80 | Set-AzureRmLoadBalancer
    ```

12. 아래의 hello 명령 hello Nic를 가져오고 hello의 각 보조 NIC toohello 백 엔드 주소 풀의 IP 구성 모두 부하 분산 장치를 추가 합니다.

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

13. 마지막으로 DNS 리소스 레코드 toopoint toohello 각 프런트 엔드 IP 주소를 hello 부하 분산 장치를 구성 해야 합니다. 도메인을 Azure DNS에 호스트할 수 있습니다. Load Balancer와 Azure DNS를 사용하는 방법에 대한 자세한 내용은 [다른 Azure 서비스와 함께 Azure DNS 사용](../dns/dns-for-azure-services.md)을 참조하세요.

## <a name="next-steps"></a>다음 단계
- 에 Azure에서 서비스 toocombine 부하 분산 방법에 대 한 자세한 [부하 분산 서비스를 사용 하 여 Azure에서](../traffic-manager/traffic-manager-load-balancing-azure.md)합니다.
- 다른 유형의 로그를 사용 하 여 Azure toomanage에 부하 분산 장치에 문제를 해결 하는 방법에 대해 알아봅니다 [Azure 부하 분산 장치에 대 한 로그 분석](../load-balancer/load-balancer-monitor-log.md)합니다.
