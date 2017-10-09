---
title: "aaaCreate Azure 내부 부하 분산 장치-PowerShell | Microsoft Docs"
description: "내부 프로그램 toocreate 리소스 관리자의 PowerShell을 사용 하 여 분산 장치를 로드 하는 방법에 대해 알아봅니다"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: c6c98981-df9d-4dd7-a94b-cc7d1dc99369
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 4b9657c77aa32a142de49ff7871ed6a396b22223
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-using-powershell"></a>PowerShell을 사용하여 내부 부하 분산 장치 만들기

> [!div class="op_single_selector"]
> * [Azure Portal](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [템플릿](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.  사용 하 여이 문서에서는 Microsoft hello 대신 대부분의 새 배포에 권장 하는 hello 리소스 관리자 배포 모델 [클래식 배포 모델](load-balancer-get-started-ilb-classic-ps.md)합니다.

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

단계를 수행 하는 hello toocreate는 내부 부하 분산 장치 Azure 리소스 관리자를 사용 하 여 PowerShell을 사용 하는 방법을 설명 합니다. Azure 리소스 관리자와 hello 항목 toocreate 내부 부하 분산 장치 개별적으로 구성 된 toocreate 부하 분산 장치를 결합 합니다.

Toocreate 필요 하 고이 정보를 개체 toodeploy 부하 분산 장치 뒤 hello를 구성 합니다.

* 프런트 엔드 IP 구성-hello 들어오는 네트워크 트래픽을 개인 IP 주소를 구성 합니다
* 백 엔드 주소 풀-프런트 엔드 IP 풀에서 들어오는 hello 부하 분산 된 트래픽을 수신할 hello 네트워크 인터페이스 구성
* 부하 분산 규칙-소스 및 로컬 포트 구성을 hello에 대 한 부하 분산 장치.
* 프로브-hello 가상 컴퓨터 인스턴스에 대 한 hello 상태 상태 프로브를 구성 합니다.
* 인바운드 NAT 규칙-hello 포트 규칙 toodirectly 액세스 hello 가상 컴퓨터 인스턴스 중 하나를 구성 합니다.

Azure 리소스 관리자의 분산 장치 구성 요소에 대한 자세한 내용은 [부하 분산 장치에 대한 Azure 리소스 관리자 지원](load-balancer-arm.md)에서 확인할 수 있습니다.

hello 다음 단계에서는 설명 방법을 tooconfigure 두 가상 컴퓨터 간에 부하 분산 장치입니다.

## <a name="setup-powershell-toouse-resource-manager"></a>PowerShell toouse 리소스 관리자를 설치 합니다.

PowerShell에 대 한 hello 최신 프로덕션 버전의 hello Azure 모듈을 있으며 올바르게 tooaccess 프로그램 Azure 구독을 설정 하는 powershell 있는지 확인 합니다.

### <a name="step-1"></a>1단계

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a>2단계

Hello 계정에 대 한 hello 구독을 확인

```powershell
Get-AzureRmSubscription
```

자격 증명으로 증명된 tooAuthenticate 됩니다.

### <a name="step-3"></a>3단계

Azure 구독 toouse 선택 합니다.

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="create-resource-group-for-load-balancer"></a>부하 분산 장치에 대한 리소스 그룹 만들기

새 리소스 그룹을 만듭니다. 기존 리소스 그룹을 사용하는 경우에는 이 단계를 건너뛰세요.

```powershell
New-AzureRmResourceGroup -Name NRP-RG -location "West US"
```

Azure 리소스 관리자를 사용하려면 모든 리소스 그룹이 위치를 지정해야 합니다. 이것은 해당 리소스 그룹의 리소스에 대 한 hello 기본 위치로 사용 됩니다. 모든 명령을 부하 분산이 사용할 toocreate hello 동일 해야 리소스 그룹입니다.

Hello 위의 예제에서는 "NRP RG" 및 "West US" 위치 라는 리소스 그룹을 만듭니다.

## <a name="create-virtual-network-and-a-private-ip-address-for-front-end-ip-pool"></a>프런트 엔드 IP 풀에 대한 개인 IP 주소 및 가상 네트워크 만들기

Hello 가상 네트워크의 서브넷을 만들고 toovariable $backendSubnet 할당

```powershell
$backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
```

가상 네트워크 만들기:

```powershell
$vnet= New-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
```

Hello 가상 네트워크를 만들고 hello 서브넷 toohello lb 서브넷 될 가상 네트워크 NRPVNet 추가 및 toovariable $vnet 할당

## <a name="create-front-end-ip-pool-and-backend-address-pool"></a>프런트 엔드 IP 풀 및 백 엔드 주소 풀 만들기

들어오는 hello에 대 한 프런트 엔드 IP 풀 설정 부하 분산 장치 네트워크 트래픽 및 백 엔드 주소 풀 tooreceive hello 부하 분산 된 트래픽을 합니다.

### <a name="step-1"></a>1단계

Hello 개인 IP 주소 10.0.2.5를 사용 하 여 hello 서브넷 10.0.2.0/24 hello 들어오는 네트워크 트래픽을 끝점 됩니다에 대 한 프런트 엔드 IP 풀을 만듭니다.

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PrivateIpAddress 10.0.2.5 -SubnetId $vnet.subnets[0].Id
```

### <a name="step-2"></a>2단계

프런트 엔드 IP 풀에서 tooreceive 들어오는 트래픽을 사용 하는 백 엔드 주소 풀을 설정 합니다.

```powershell
$beaddresspool= New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
```

## <a name="create-lb-rules-nat-rules-probe-and-load-balancer"></a>LB 규칙, NAT 규칙, 프로브 및 부하 분산 장치 만들기

Hello 프런트 엔드 IP 풀 및 hello 백 엔드 주소 풀을 만든 후 toohello 부하 분산 장치 리소스가 속하는 toocreate hello 규칙이 필요 합니다.

### <a name="step-1"></a>1단계

```powershell
$inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP1" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

$inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP2" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389

$healthProbe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -RequestPath "HealthProbe.aspx" -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name "HTTP" -FrontendIpConfiguration $frontendIP -BackendAddressPool $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
```

위의 hello 예에는 다음 항목 hello 생성은:

* 들어오는 모든 트래픽을 tooport 3441는 NAT 규칙은 tooport 3389 이동 합니다.
* 두 번째 NAT 규칙을 들어오는 모든 트래픽을 tooport 3442 tooport 3389 이동 합니다.
* 로드 하는 부하 분산 장치 규칙 hello 백 엔드 주소 풀에 공용 포트 80 toolocal 포트 80에 들어오는 모든 트래픽을 조정 합니다.
* hello "HealthProbe.aspx" 경로 대 한 상태를 확인 하는 검색 규칙

### <a name="step-2"></a>2단계

모든 개체 (예: NAT 규칙, 부하 분산 장치 규칙, 프로브 구성)을 함께 추가 하는 hello 부하 분산 장치를 만듭니다.

```powershell
$NRPLB = New-AzureRmLoadBalancer -ResourceGroupName "NRP-RG" -Name "NRP-LB" -Location "West US" -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
```

## <a name="create-network-interfaces"></a>네트워크 인터페이스 만들기

Hello 내부 부하 분산 장치를 만든 후 네트워크 인터페이스 수신할 hello 수신 부하 분산 된 네트워크 트래픽 NAT 규칙 및 프로브 정의 해야 합니다. hello 네트워크 인터페이스가 경우 개별적으로 구성 하며 지정할 수 있습니다 tooa 가상 컴퓨터 나중에 있습니다.

### <a name="step-1"></a>1단계

Hello 리소스를 가상 네트워크 및 서브넷 toocreate 네트워크 인터페이스 가져오기:

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG

$backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
```

이 단계에서는 toohello 부하 분산 장치 백 엔드 풀에 속한이 네트워크 인터페이스에 대 한 RDP에 대 한 hello 첫 번째 NAT 규칙을 연결 하는 네트워크 인터페이스를 만듭니다.

```powershell
$backendnic1= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic1-be -Location "West US" -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
```

### <a name="step-2"></a>2단계

LB-Nic2-BE라는 두 번째 네트워크 인터페이스 만들기:

이 단계에서는 두 번째 네트워크 인터페이스, 할당 toohello 동일한 부하 분산 장치 다시 풀을 종료 하 고 rdp 만든 hello 두 번째 NAT 규칙 연결:

```powershell
$backendnic2= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic2-be -Location "West US" -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
```

hello 최종 결과 hello 다음을 표시 됩니다.

    $backendnic1

예상 출력:

    Name                 : lb-nic1-be
    ResourceGroupName    : NRP-RG
    Location             : westus
    Id                   : /subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
    Etag                 : W/"d448256a-e1df-413a-9103-a137e07276d1"
    ProvisioningState    : Succeeded
    Tags                 :
    VirtualMachine       : null
    IpConfigurations     : [
                         {
                           "PrivateIpAddress": "10.0.2.6",
                           "PrivateIpAllocationMethod": "Static",
                           "Subnet": {
                             "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/virtualNetworks/NRPVNet/subnets/LB-Subnet-BE"
                           },
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
                           "ProvisioningState": "Succeeded",
                           "Name": "ipconfig1",
                           "Etag": "W/\"d448256a-e1df-413a-9103-a137e07276d1\"",
                           "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/ipconfig1"
                         }
                       ]
    DnsSettings          : {
                         "DnsServers": [],
                         "AppliedDnsServers": []
                       }
    AppliedDnsSettings   :
    NetworkSecurityGroup : null
    Primary              : False



### <a name="step-3"></a>3단계

Hello 명령 추가 AzureRmVMNetworkInterface tooassign hello NIC tooa 가상 컴퓨터를 사용 합니다.

가상 컴퓨터를 위한 단계별 지침 toocreate hello와 NIC tooa 할당 찾을 수 있습니다 hello 설명서: [PowerShell을 사용 하는 Azure VM 만들기](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)합니다.

## <a name="add-hello-network-interface"></a>Hello 네트워크 인터페이스를 추가 합니다.

만든 가상 컴퓨터가 이미 있는 경우에 단계를 수행 하는 hello로 hello 네트워크 인터페이스를 추가할 수 있습니다.

### <a name="step-1"></a>1단계

(아직 수행 하지 않은) 하는 경우 변수를 hello 부하 분산 장치 리소스를 로드 합니다. hello 사용 되는 변수가 호출된 $lb 하 고 위에서 만든 hello 부하 분산 장치 리소스에서 동일한 이름을 사용 하 여 hello 합니다.

```powershell
$lb = Get-AzureRmLoadBalancer –name NRP-LB -resourcegroupname NRP-RG
```

### <a name="step-2"></a>2단계

Hello 백 엔드 구성 tooa 변수에 로드 합니다.

```powershell
$backend = Get-AzureRmLoadBalancerBackendAddressPoolConfig -name backendpool1 -LoadBalancer $lb
```

### <a name="step-3"></a>3단계

변수를 이미 만든 hello 네트워크 인터페이스를 로드 합니다. 사용 되는 변수 이름 hello $nic.은 hello 네트워크 인터페이스 이름을 사용 하는 위의 hello 예제에서 hello 동일 합니다.

```powershell
$nic = Get-AzureRmNetworkInterface –name lb-nic1-be -resourcegroupname NRP-RG
```

### <a name="step-4"></a>4단계

Hello 네트워크 인터페이스에서 hello 백 엔드 구성을 변경 합니다.

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
```

### <a name="step-5"></a>5단계

Hello 네트워크 인터페이스 개체를 저장 합니다.

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

네트워크 인터페이스 toohello 부하 분산 장치 백 엔드 풀을 추가한 다음 해당 부하 분산 장치 리소스에 대 한 규칙을 분산 하는 hello 부하에 따라 네트워크 트래픽을 받기 시작 합니다.

## <a name="update-an-existing-load-balancer"></a>기존 부하 분산 장치 업데이트

### <a name="step-1"></a>1단계
부하 분산 장치 개체 toovariable $slb AzureRmLoadBalancer Get를 사용 하 여 할당 위의 hello 예제에서 hello 부하 분산 장치를 사용 하 여

```powershell
$slb = Get-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

### <a name="step-2"></a>2단계

다음 예제는 hello에서 포트 81에 hello 프런트 엔드를 사용 하 여 새 인바운드 NAT 규칙을 추가 합니다 및 포트 8181 hello 다시의 종료 시간 풀 tooan 기존 부하 분산 장치

```powershell
$slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol Tcp
```

### <a name="step-3"></a>3단계

AzureLoadBalancer 집합을 사용 하 여 hello 새 구성을 저장 합니다.

```powershell
$slb | Set-AzureRmLoadBalancer
```

## <a name="remove-a-load-balancer"></a>부하 분산 장치 제거하기

Hello 명령 제거 AzureRmLoadBalancer toodelete "NRP 파운드" 리소스 그룹의 "NRP RG" 라는 명명 된 이전에 만든된 부하 분산 장치를 사용 하 여

```powershell
Remove-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

> [!NOTE]
> Hello 옵션을 사용할 수 있습니다 스위치-Force tooavoid hello 프롬프트 삭제 합니다.

## <a name="next-steps"></a>다음 단계

[부하 분산 장치 배포 모드 구성](load-balancer-distribution-mode.md)

[부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성](load-balancer-tcp-idle-timeout.md)
