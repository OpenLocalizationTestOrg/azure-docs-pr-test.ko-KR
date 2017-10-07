---
title: "Azure 가상 네트워크에 대 한 PowerShell aaaCommon 명령을 | Microsoft Docs"
description: "일반적인 PowerShell 명령 tooget Vm에 대 한 가상 네트워크와 연결된 된 리소스를 만들기 시작 합니다."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 56e1a73c-8299-4996-bd03-f74585caa1dc
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: b46b78f1b7c5a0c5ba917fb48f568d871e5e8789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="common-powershell-commands-for-azure-virtual-networks"></a>Azure Virtual Networks에 대한 공통 PowerShell 명령

Toocreate toocreate 가상 컴퓨터를 원하는 경우 해야는 [가상 네트워크](../../virtual-network/virtual-networks-overview.md) 나 기존 가상 네트워크에 대 한 알고 있는 hello VM을 추가할 수 있습니다. 일반적으로 VM을 만들 때 있어야이 문서에서 설명 하는 hello 리소스를 만드는 tooconsider 합니다.

참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) hello 최신 버전의 Azure PowerShell을 설치, 구독을 선택 하 고 tooyour 계정에 로그인 하는 방법에 대 한 정보에 대 한 합니다.

이 문서에 둘 이상의 hello 명령을 실행 하는 경우 일부 변수 두면 유용할 수 있습니다.

- $location-hello 네트워크 리소스의 hello 위치입니다. 사용할 수 있습니다 [Get AzureRmLocation](https://docs.microsoft.com/powershell/module/azurerm.resources/get-azurermlocation) toofind는 [지리적 지역의](https://azure.microsoft.com/regions/) 있는 주시기 바랍니다.
- $myResourceGroup-hello 네트워크 리소스를 찾는 hello 리소스 그룹의 hello 이름입니다.

## <a name="create-network-resources"></a>네트워크 리소스 만들기

| 작업 | 명령 |
| ---- | ------- |
| 서브넷 구성 만들기 |$subnet1 = [New-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) -Name "mySubnet1" -AddressPrefix XX.X.X.X/XX<BR>$subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnet2" -AddressPrefix XX.X.X.X/XX<BR><BR>일반적인 네트워크는 [인터넷 연결 부하 분산 장치](../../load-balancer/load-balancer-internet-overview.md)에 대한 서브넷 및 [내부 부하 분산 장치](../../load-balancer/load-balancer-internal-overview.md)에 대한 별도 서브넷을 가질 수도 있습니다. |
| 가상 네트워크 만들기 |$vnet = [New-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermvirtualnetwork) -Name "myVNet" -ResourceGroupName $myResourceGroup -Location $location -AddressPrefix XX.X.X.X/XX -Subnet $subnet1, $subnet2 |
| 고유한 도메인 이름에 대한 테스트 |[Test-AzureRmDnsAvailability](https://docs.microsoft.com/powershell/module/azurerm.network/test-azurermdnsavailability) -DomainNameLabel "myDNS" -Location $location<BR><BR>에 대 한 DNS 도메인 이름을 지정할 수 있습니다는 [공용 IP 리소스](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)를 만듦 domainname.location.cloudapp.azure.com toohello 공용 IP 주소에 대 한 매핑을 hello에 Azure 관리 되는 DNS 서버입니다. hello 이름은 문자, 숫자 및 하이픈만 포함할 수 있습니다. hello 첫 자와 끝 자는 문자 또는 숫자 여야 합니다 및 hello 도메인 이름은 Azure 위치 내에서 고유 해야 합니다. **True** 가 반환된 경우 제안한 이름이 전역적으로 고유합니다. |
| 공용 IP 주소 만들기 |$pip = [New-AzureRmPublicIpAddress](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermpublicipaddress) -Name "myPublicIp" -ResourceGroupName $myResourceGroup -DomainNameLabel "myDNS" -Location $location -AllocationMethod Dynamic<BR><BR>hello 공용 IP 주소에는 이전에 테스트 하 고 hello hello 부하 분산 장치 프런트 엔드 구성에 의해 사용 된 hello 도메인 이름을 사용 합니다. |
| 프런트 엔드 IP 구성 만들기 |$frontendIP = [New-AzureRmLoadBalancerFrontendIpConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) -Name "myFrontendIP" -PublicIpAddress $pip<BR><BR>hello 프런트 엔드 구성은 이전에 만든 들어오는 네트워크 트래픽을 hello 공용 IP 주소를 포함 합니다. |
| 백 엔드 주소 풀 만들기 |$beAddressPool = [New-AzureRmLoadBalancerBackendAddressPoolConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) -Name "myBackendAddressPool"<BR><BR>Hello 백 엔드의 hello에 대 한 내부 주소 부하 분산 장치 네트워크 인터페이스를 통해 액세스할 수 있는 제공 합니다. |
| 프로브 만들기 |$healthProbe = [New-AzureRmLoadBalancerProbeConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) -Name "myProbe" -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2<BR><BR>Hello 백 엔드 주소 풀에 있는 가상 컴퓨터 인스턴스의 사용 된 검색 toocheck 가용성 상태를 포함합니다. |
| 부하 분산 규칙 만들기 |$lbRule = [New-AzureRmLoadBalancerRuleConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) -Name HTTP -FrontendIpConfiguration $frontendIP -BackendAddressPool $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80<BR><BR>Hello 백 엔드 주소 풀의 tooa 포트 hello 부하 분산 장치에 공용 포트를 할당 하는 규칙을 포함 합니다. |
| 인바운드 NAT 규칙 만들기 |$inboundNATRule = [New-AzureRmLoadBalancerInboundNatRuleConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerinboundnatruleconfig) -Name "myInboundRule1" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389<BR><BR>Hello hello 백 엔드 주소 풀에서 특정 가상 컴퓨터에 대 한 부하 분산 장치 tooa 포트에 공용 포트 매핑 규칙을 포함 합니다. |
| 부하 분산 장치 만들기 |$loadBalancer = [New-AzureRmLoadBalancer](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancer) -ResourceGroupName $myResourceGroup -Name "myLoadBalancer" -Location $location -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule -LoadBalancingRule $lbRule -BackendAddressPool $beAddressPool -Probe $healthProbe |
| 네트워크 인터페이스 만들기 |$nic1= [New-AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermnetworkinterface) -ResourceGroupName $myResourceGroup -Name "myNIC" -Location $location -PrivateIpAddress XX.X.X.X -Subnet $subnet2 -LoadBalancerBackendAddressPool $loadBalancer.BackendAddressPools[0] -LoadBalancerInboundNatRule $loadBalancer.InboundNatRules[0]<BR><BR>Hello 공용 IP 주소와 이전에 만든 가상 네트워크 서브넷을 사용 하 여 네트워크 인터페이스를 만듭니다. |

## <a name="get-information-about-network-resources"></a>네트워크 리소스에 대한 정보 가져오기

| 작업 | 명령 |
| ---- | ------- |
| 가상 네트워크 나열 |[Get-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermvirtualnetwork) -ResourceGroupName $myResourceGroup<BR><BR>Hello 리소스 그룹에 모든 hello 가상 네트워크를 나열합니다. |
| 가상 네트워크에 대한 정보 가져오기 |Get-AzureRmVirtualNetwork -Name "myVNet" -ResourceGroupName $myResourceGroup |
| 가상 네트워크의 서브넷 나열 |Get-AzureRmVirtualNetwork -Name "myVNet" -ResourceGroupName $myResourceGroup &#124; Select Subnets |
| 서브넷에 대한 정보 가져오기 |[Get-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) -Name "mySubnet1" -VirtualNetwork $vnet<BR><BR>Hello 지정 된 가상 네트워크의 서브넷 hello에 대 한 정보를 가져옵니다. hello $vnet 값 AzureRmVirtualNetwork Get에서 반환 하는 hello 개체를 나타냅니다. |
| IP 주소 나열 |[Get-AzureRmPublicIpAddress](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermpublicipaddress) -ResourceGroupName $myResourceGroup<BR><BR>Hello hello 리소스 그룹에 공용 IP 주소를 나열합니다. |
| 부하 분산 장치 나열 |[Get-AzureRmLoadBalancer](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermloadbalancer) -ResourceGroupName $myResourceGroup<BR><BR>Hello 리소스 그룹에 모든 hello 부하 분산 장치를 나열합니다. |
| 네트워크 인터페이스 나열 |[Get-AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermnetworkinterface) -ResourceGroupName $myResourceGroup<BR><BR>Hello 리소스 그룹의 모든 hello 네트워크 인터페이스를 나열합니다. |
| 네트워크 인터페이스에 대한 정보 가져오기 |Get-AzureRmNetworkInterface -Name "myNIC" -ResourceGroupName $myResourceGroup<BR><BR>특정 네트워크 인터페이스에 대한 정보를 가져옵니다. |
| 네트워크 인터페이스의 hello IP 구성 가져오기 |[Get-AzureRmNetworkInterfaceIPConfig](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermnetworkinterfaceipconfig) -Name "myNICIP" -NetworkInterface $nic<BR><BR>Hello 지정 된 네트워크 인터페이스의 hello IP 구성에 대 한 정보를 가져옵니다. hello $nic 값 AzureRmNetworkInterface Get에서 반환 하는 hello 개체를 나타냅니다. |

## <a name="manage-network-resources"></a>네트워크 리소스 관리

| 작업 | 명령 |
| ---- | ------- |
| 서브넷 tooa 가상 네트워크 추가 |[Add-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig) -AddressPrefix XX.X.X.X/XX -Name "mySubnet1" -VirtualNetwork $vnet<BR><BR>서브넷 tooan 기존 가상 네트워크를 추가합니다. hello $vnet 값 AzureRmVirtualNetwork Get에서 반환 하는 hello 개체를 나타냅니다. |
| 가상 네트워크 삭제 |[Remove-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/module/azurerm.network/remove-azurermvirtualnetwork) -Name "myVNet" -ResourceGroupName $myResourceGroup<BR><BR>Hello 리소스 그룹에서 가상 네트워크를 지정된 하는 hello를 제거합니다. |
| 네트워크 인터페이스 삭제 |[Remove-AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.network/remove-azurermnetworkinterface) -Name "myNIC" -ResourceGroupName $myResourceGroup<BR><BR>지정 된 네트워크 인터페이스 hello hello 리소스 그룹에서 제거합니다. |
| 부하 분산 장치 삭제 |[Remove-AzureRmLoadBalancer](https://docs.microsoft.com/powershell/module/azurerm.network/remove-azurermloadbalancer) -Name "myLoadBalancer" -ResourceGroupName $myResourceGroup<BR><BR>제거 hello hello 리소스 그룹에서 부하 분산 장치를 지정 합니다. |
| 공용 IP 주소 삭제 |[Remove-AzureRmPublicIpAddress](https://docs.microsoft.com/powershell/module/azurerm.network/remove-azurermpublicipaddress)-Name "myIPAddress" -ResourceGroupName $myResourceGroup<BR><BR>제거 hello hello 리소스 그룹에서 공용 IP 주소를 지정 합니다. |

## <a name="next-steps"></a>다음 단계
* 방금 사용 하 여 hello 네트워크 인터페이스를 만들 때 있습니다 [VM을 만들](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.
* [여러 네트워크 인터페이스를 사용하여 VM 만들기](../../virtual-network/virtual-networks-multiple-nics.md)를 할 수 있는 방법을 알아봅니다.

