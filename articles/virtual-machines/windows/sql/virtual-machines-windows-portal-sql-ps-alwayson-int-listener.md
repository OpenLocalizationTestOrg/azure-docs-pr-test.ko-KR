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
# <a name="configure-one-or-more-always-on-availability-group-listeners---resource-manager"></a>하나 이상의 Always On 가용성 그룹 수신기 구성 - Resource Manager
이 문서에서는 다음을 수행하는 방법을 보여 줍니다.

* PowerShell cmdlet을 사용하여 SQL Server 가용성 그룹에 대한 내부 부하 분산 장치를 만듭니다.
* 여러 가용성 그룹에 대 한 추가 IP 주소 tooa 부하 분산을 추가 합니다. 

가용성 그룹 수신기는 클라이언트가 연결할 toofor 데이터베이스 액세스는 가상 네트워크 이름입니다. Azure 가상 컴퓨터에 부하 분산 장치는 hello 수신기에 대 한 hello IP 주소를 보유합니다. hello 부하 분산 장치 경로 트래픽 toohello SQL Server 인스턴스의 hello 프로브 포트에서 수신 합니다. 일반적으로 가용성 그룹은 내부 부하 분산 장치를 사용합니다. Azure 내부 부하 분산 장치는 하나 이상의 IP 주소를 호스트할 수 있습니다. 각 IP 주소는 특정 프로브 포트를 사용합니다. 이 문서에서는 어떻게 toouse PowerShell toocreate 부하 분산 장치 또는 IP 주소 tooan 기존 SQL Server 가용성 그룹에 대 한 부하 분산 장치를 추가 합니다. 

hello 기능 tooassign 여러 IP 주소 tooan 내부 부하 분산 장치 새 tooAzure 이며 리소스 관리자 모델에서 사용할 수만 있습니다. toocomplete toohave SQL Server 가용성 그룹 리소스 관리자 모델에서 Azure 가상 컴퓨터에 배포 해야이 작업을 합니다. SQL Server 가상 컴퓨터 둘 다 toohello 속해야 합니다. 동일한 가용성 집합입니다. Hello를 사용할 수 있습니다 [Microsoft 템플릿](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) tooautomatically Azure 리소스 관리자의 hello 가용성 그룹을 만듭니다. 이 서식 파일에는 자동으로 hello 내부 부하 분산 장치를 포함 하 여 hello 가용성 그룹을 만듭니다. 원하는 경우 [수동으로 Always On 가용성 그룹을 구성](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)할 수 있습니다.

이 항목을 수행하려면 가용성 그룹이 이미 구성되어 있어야 합니다.  

관련 항목은 다음과 같습니다.

* [Azure VM의 Always On 가용성 그룹 구성(GUI)](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [Azure 리소스 관리자 및 PowerShell을 사용하여 VNet-VNet 연결 구성](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

[!INCLUDE [Start your PowerShell session](../../../../includes/sql-vm-powershell.md)]

## <a name="configure-hello-windows-firewall"></a>Hello Windows 방화벽 구성
Hello Windows 방화벽 tooallow SQL Server 액세스를 구성 합니다. hello 방화벽 규칙 TCP 연결 toohello 포트 hello SQL Server 인스턴스 및 hello 수신기 프로브 여 사용할 수 있습니다. 자세한 지침은 [데이터베이스 엔진 액세스를 위해 Windows 방화벽 구성](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1)을 참조하세요. Hello 프로브 포트 및 SQL Server 포트 hello에 대 한 인바운드 규칙을 만듭니다.

## <a name="example-script-create-an-internal-load-balancer-with-powershell"></a>예제 스크립트: PowerShell을 사용하여 내부 부하 분산 장치 만들기
> [!NOTE]
> Hello를 사용 하 여 가용성 그룹을 만든 경우 [Microsoft 템플릿](virtual-machines-windows-portal-sql-alwayson-availability-groups.md), hello 내부 부하 분산 장치 이미 만들었습니다. 
> 
> 

hello 다음 PowerShell 스크립트는 내부 부하 분산 장치, 구성 hello 부하 분산 규칙을 만들고 hello 부하 분산 장치에 대 한 IP 주소를 설정 합니다. toorun hello 스크립트를 Windows PowerShell ISE를 열고 hello 스크립트 hello 스크립트 창에 붙여 넣습니다. 사용 하 여 `Login-AzureRMAccount` toolog tooPowerShell에 있습니다. 여러 Azure 구독이 있으면 사용 하 여 `Select-AzureRmSubscription ` tooset hello 구독 합니다. 

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

## <a name="Add-IP"></a>스크립트 예:는 IP 주소 tooan 기존 부하 분산 장치 추가 powershell
toouse 두 개 이상의 하나의 가용성 그룹에서 추가 IP 주소 toohello 부하 분산 장치를 추가 합니다. 각 IP 주소에는 자체 부하 분산 규칙, 프로브 포트 및 프런트 엔드 포트가 필요합니다.

hello 프런트 엔드 포트는 응용 프로그램 tooconnect toohello SQL Server 인스턴스를 사용 하는 hello 포트입니다. 다른 가용성 그룹을 사용 하 여 수에 대 한 IP 주소 hello 동일한 프런트 엔드 포트입니다.

> [!NOTE]
> SQL Server 가용성 그룹의 경우 각 IP 주소에 특정 프로브 포트가 필요합니다. 예를 들어 부하 분산 장치에 있는 하나의 IP 주소가 프로브 포트 59999를 사용하는 경우 해당 부하 분산 장치의 다른 IP 주소는 프로브 포트 59999를 사용할 수 없습니다.

* 부하 분산 장치 제한에 대한 자세한 내용은 **네트워킹 제한 - Azure Resource Manager**에서 [부하 분산 장치당 개인 프런트 엔드 IP](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits)를 참조하세요.
* 가용성 그룹 제한에 대한 자세한 내용은 [제한 사항(가용성 그룹)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG)을 참조하세요.

hello 다음 스크립트 추가 새 IP 주소 tooan 기존 부하 분산 장치입니다. ILB hello hello 부하 분산 프런트 엔드 포트에 대 한 hello 수신기 포트를 사용 합니다. 이 포트에서 수신 대기 중인 SQL Server hello 포트 수 있습니다. SQL Server의 기본 인스턴스의 경우 hello 포트는 1433입니다. hello 부하 분산 가용성 그룹에 대 한 규칙 부동 IP (직접 서버 반환) hello 백 엔드 포트 이므로 hello 동일 hello 프런트 엔드 포트와 필요 합니다. 사용자 환경에 대 한 hello 변수를 업데이트 합니다. 

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

## <a name="configure-hello-listener"></a>Hello 수신기 구성

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-hello-listener-port-in-sql-server-management-studio"></a>SQL Server Management Studio에서 hello 수신기 포트를 설정 합니다.

1. SQL Server Management Studio를 시작 하 고 toohello 주 복제본에 연결 합니다.

1. 너무 이동**AlwaysOn 고가용성** | **가용성 그룹** | **가용성 그룹 수신기**합니다. 

1. 이제 장애 조치 클러스터 관리자에서 만든 hello 수신기 이름이 표시 됩니다. Hello 수신기 이름을 마우스 오른쪽 단추로 클릭 하 고 클릭 **속성**합니다.

1. Hello에 **포트** 상자 이전 사용 $EndpointPort hello를 사용 하 여 hello 가용성 그룹 수신기에 대 한 hello 포트 번호를 지정 합니다 (1433 hello이 기본값 이었습니다)를 클릭 한 다음 **확인**합니다.

## <a name="test-hello-connection-toohello-listener"></a>테스트 hello 연결 toohello 수신기

tootest hello 연결:

1. RDP tooa SQL 서버 hello에 있는 동일한 가상 네트워크 구성 요소, 않도록 지정 되었으나 자체 hello 복제 합니다. Hello 클러스터의 다른 SQL Server를 hello 수이 있습니다.

1. 사용 하 여 **sqlcmd** 유틸리티 tootest hello 연결 합니다. 예를 들어 다음 스크립트는 hello 설정는 **sqlcmd** hello 수신기 Windows 인증을 통해 연결 toohello 주 복제본:
   
    ```
    sqlmd -S <listenerName> -E
    ```
   
    Hello 수신기 포트를 사용 하는 이외의 경우 hello 기본 포트 (1433)를 hello 연결 문자열에 hello 포트를 지정 합니다. 예를 들어 hello 다음 sqlcmd 명령을 연결 tooa 수신기 포트 1435에서: 
   
    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

hello SQLCMD 연결 toowhichever 인스턴스의 SQL Server 호스트 hello에 대 한 주 복제본을 자동으로 연결합니다. 

> [!NOTE]
> 지정한 hello 포트가 두 SQL Server의 hello 방화벽에서 열려 있는지 확인 합니다. 두 서버 hello 있습니다를 사용 하는 TCP 포트에 대 한 인바운드 규칙을 필요로 합니다. 자세한 내용은 [방화벽 규칙 추가 또는 편집](http://technet.microsoft.com/library/cc753558.aspx)을 참조하세요. 
> 
> 

## <a name="guidelines-and-limitations"></a>지침 및 제한 사항
내부 부하 분산 장치를 사용 하 여 Azure에서 가용성 그룹 수신기에 대 한 지침을 따라 참고 hello:

* 내부 부하 분산 장치,만 hello 내에서 hello 수신기가 액세스할 동일한 가상 네트워크입니다.


## <a name="for-more-information"></a>Blob에 대한 자세한 내용은
자세한 내용은 [수동으로 Azure VM의 Always On 가용성 그룹 구성](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)을 참조하세요.

## <a name="powershell-cmdlets"></a>PowerShell cmdlet
다음 PowerShell cmdlet toocreate Azure 가상 컴퓨터에 대 한 내부 부하 분산 장치는 hello를 사용 합니다.

* [New-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt619450.aspx)는 부하 분산 장치를 만듭니다. 
* [New-AzureRMLoadBalancerFrontendIpConfig](http://msdn.microsoft.com/library/mt603510.aspx)는 부하 분산 장치에 대한 프런트 엔드 IP 구성을 만듭니다. 
* [New-AzureRmLoadBalancerRuleConfig](http://msdn.microsoft.com/library/mt619391.aspx)는 부하 분산 장치에 대한 규칙 구성을 만듭니다. 
* [New-AzureRmLoadBalancerBackendAddressPoolConfig](http://msdn.microsoft.com/library/mt603791.aspx)는 부하 분산 장치에 대한 백 엔드 주소 풀 구성을 만듭니다. 
* [New-AzureRmLoadBalancerProbeConfig](http://msdn.microsoft.com/library/mt603847.aspx)는 부하 분산 장치에 대한 프로브 구성을 만듭니다.
* [Remove-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx)는 Azure 리소스 그룹에서 부하 분산 장치를 제거합니다.
