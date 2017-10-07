---
title: "Azure에서 SAP SID 다중 구성은 aaaCreate | Microsoft Docs"
description: "Windows 가상 컴퓨터에 가이드 toohigh 가용성 SAP NetWeaver 다중 SID 구성"
services: virtual-machines-windows, virtual-network, storage
documentationcenter: saponazure
author: goraco
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 0b89b4f8-6d6c-45d7-8d20-fe93430217ca
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/05/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e2a4b12928231743c59af86dab72595ad38d364b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-sap-netweaver-multi-sid-configuration"></a>SAP NetWeaver 다중 SID 구성 만들기

[load-balancer-multivip-overview]:../../../load-balancer/load-balancer-multivip-overview.md
[sap-ha-guide]:sap-high-availability-guide.md 
[sap-ha-guide-figure-6001]:./media/virtual-machines-shared-sap-high-availability-guide/6001-sap-multi-sid-ascs-scs-sid1.png
[sap-ha-guide-figure-6002]:./media/virtual-machines-shared-sap-high-availability-guide/6002-sap-multi-sid-ascs-scs.png
[sap-ha-guide-figure-6003]:./media/virtual-machines-shared-sap-high-availability-guide/6003-sap-multi-sid-full-landscape.png
[sap-ha-guide-figure-6004]:./media/virtual-machines-shared-sap-high-availability-guide/6004-sap-multi-sid-dns.png
[sap-ha-guide-figure-6005]:./media/virtual-machines-shared-sap-high-availability-guide/6005-sap-multi-sid-azure-portal.png
[sap-ha-guide-figure-6006]:./media/virtual-machines-shared-sap-high-availability-guide/6006-sap-multi-sid-sios-replication.png
[networking-limits-azure-resource-manager]:../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits
[sap-ha-guide-9.1.1]:sap-high-availability-guide.md#a97ad604-9094-44fe-a364-f89cb39bf097 
[sap-ha-guide-8.8]:sap-high-availability-guide.md#f19bd997-154d-4583-a46e-7f5a69d0153c
[sap-ha-guide-8.12.3.3]:sap-high-availability-guide.md#d9c1fc8e-8710-4dff-bec2-1f535db7b006 
[sap-ha-guide-9]:sap-high-availability-guide.md#a06f0b49-8a7a-42bf-8b0d-c12026c5746b
[sap-ha-guide-9.1]:sap-high-availability-guide.md#31c6bd4f-51df-4057-9fdf-3fcbc619c170 
[sap-ha-guide-9.1.2]:sap-high-availability-guide.md#eb5af918-b42f-4803-bb50-eff41f84b0b0 
[sap-ha-guide-9.1.3]:sap-high-availability-guide.md#e4caaab2-e90f-4f2c-bc84-2cd2e12a9556 
[sap-ha-guide-9.1.4]:sap-high-availability-guide.md#10822f4f-32e7-4871-b63a-9b86c76ce761 
[sap-ha-guide-9.4]:sap-high-availability-guide.md#094bc895-31d4-4471-91cc-1513b64e406a 
[sap-ha-guide-9.5]:sap-high-availability-guide.md#2477e58f-c5a7-4a5d-9ae3-7b91022cafb5 
[sap-ha-guide-9.6]:sap-high-availability-guide.md#0ba4a6c1-cc37-4bcf-a8dc-025de4263772 
[sap-ha-guide-10]:sap-high-availability-guide.md#18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9

2016년 9월에 Microsoft는 Azure 내부 부하 분산 장치를 사용하여 여러 가상 IP 주소를 관리할 수 있는 기능을 릴리스했습니다. 이 기능은 hello Azure 외부 부하 분산 장치에 이미 있습니다.

SAP 배포를 설정한 경우 사용할 수 있습니다 Windows 클러스터 구성에는 내부 부하 분산 장치 toocreate SAP ASCS/SCS에 대 한 hello에 설명 된 대로 [Windows Vm에서 SAP NetWeaver 고가용성에 대 한 가이드] [ sap-ha-guide].

이 문서는 toomove 단일 ASCS/SCS 설치 tooan SAP SID 다중 구성에서 추가 SAP ASCS/SCS를 설치 하 여 기존 Windows Server 장애 조치 클러스터링 (WSFC) 클러스터에 인스턴스를 클러스터링 하는 방법에 중점을 둡니다. 이 프로세스가 완료되면 SAP 다중 SID 클러스터가 구성됩니다.


## <a name="prerequisites"></a>필수 조건
이미 구성한 한 SAP ASCS/SCS 인스턴스에 사용 되는 WSFC 클러스터 hello에 설명 된 대로 [Windows Vm에서 SAP NetWeaver 고가용성에 대 한 가이드] [ sap-ha-guide] 이 다이어그램에 나와 있는 것 처럼 및 합니다.

![고가용성 SAP ASCS/SCS 인스턴스][sap-ha-guide-figure-6001]

## <a name="target-architecture"></a>대상 아키텍처

hello ´ ֲ ° hello에 tooinstall 여러 SAP ABAP ASCS 또는 SAP Java SCS 클러스터 된 인스턴스의 동일한 WSFC 클러스터에서 다음과 같이 합니다.

![Azure에서 여러 SAP ASCS/SCS 클러스터링된 인스턴스][sap-ha-guide-figure-6002]

> [!NOTE]
>각 Azure 내부 부하 분산 장치에 대 한 프런트 엔드 개인 ip 제한 toohello 수가입니다.
>
>한 WSFC 클러스터에 있는 SAP ASCS/SCS 인스턴스의 hello 최대 수는 각 Azure 내부 부하 분산 장치에 대 한 프런트 엔드 개인 Ip의 최대 수를 같은 toohello 합니다.
>

부하 분산 장치 제한에 대한 자세한 내용은 [네트워킹 제한 - Azure Resource Manager][networking-limits-azure-resource-manager]에서 “부하 분산 장치당 개인 프런트 엔드 IP”를 참조하세요.

두 개의 고가용성 SAP 시스템과 hello 전체 가로 다음과 같습니다.

![두 개의 SAP 시스템 SID를 포함한 SAP 고가용성 다중 SID 설치 프로그램][sap-ha-guide-figure-6003]

> [!IMPORTANT]
> hello 설치 hello 다음 조건을 충족 해야 합니다.
> - hello SAP ASCS/SCS 인스턴스를 공유 해야 hello 동일한 WSFC 클러스터입니다.
> - 각 DBMS SID에는 해당하는 고유한 전용 WSFC 클러스터가 있어야 합니다.
> - Tooone SAP 시스템 SID 속해 있는 SAP 응용 프로그램 서버에 자체 전용된 Vm 있어야 합니다.


## <a name="prepare-hello-infrastructure"></a>Hello 인프라 준비
tooprepare 인프라에 매개 변수 뒤 hello로 추가 SAP ASCS/SCS 인스턴스를 설치할 수 있습니다.

| 매개 변수 이름 | 값 |
| --- | --- |
| SAP ASCS/SCS SID |pr1-lb-ascs |
| SAP DBMS 내부 부하 분산 장치 | PR5 |
| SAP 가상 호스트 이름 | pr5-sap-cl |
| SAP ASCS/SCS 가상 호스트 IP 주소(추가 Azure Load Balancer IP 주소) | 10.0.0.50 |
| SAP ASCS/SCS 인스턴스 번호 | 50 |
| 추가 SAP ASCS/SCS 인스턴스의 ILB 프로브 포트 | 62350 |

> [!NOTE]
> SAP ASCS/SCS 클러스터 인스턴스의 경우 각 IP 주소에는 고유한 프로브 포트가 필요합니다. 예를 들어 Azure 내부 부하 분산 장치에 있는 하나의 IP 주소가 프로브 포트 62300을 사용하는 경우 해당 부하 분산 장치의 다른 IP 주소는 프로브 포트 62300을 사용할 수 없습니다.
>
>프로브 포트 62300이 이미 예약되어 있으므로 여기서는 프로브 포트 62350을 사용하고 있습니다.

두 개의 노드가 있는 hello 기존 WSFC 클러스터의 추가 SAP ASCS/SCS 인스턴스를 설치할 수 있습니다.

| 가상 컴퓨터 역할 | 가상 컴퓨터 호스트 이름 | 고정 IP 주소 |
| --- | --- | --- |
| ASCS/SCS 인스턴스의 첫 번째 클러스터 노드 |pr1-ascs-0 |10.0.0.10 |
| ASCS/SCS 인스턴스의 두 번째 클러스터 노드 |pr1-ascs-1 |10.0.0.9 |

### <a name="create-a-virtual-host-name-for-hello-clustered-sap-ascsscs-instance-on-hello-dns-server"></a>Hello DNS 서버에서 클러스터 된 hello SAP ASCS/SCS 인스턴스의 가상 호스트 이름을 만들기

매개 변수 뒤 hello를 사용 하 여 hello ASCS/SCS 인스턴스의 hello 가상 호스트 이름에 대 한 DNS 항목을 만들 수 있습니다.

| 새 SAP ASCS/SCS 가상 호스트 이름 | 연결된 IP 주소 |
| --- | --- | --- |
|pr5-sap-cl |10.0.0.50 |

다음 스크린 샷에서 hello와 같이 hello 새 호스트 이름과 IP 주소가 hello DNS 관리자에에서 표시 됩니다.

![Hello를 강조 표시 하는 DNS 관리자 목록 정의 hello 새 SAP ASCS/SCS 클러스터 가상 이름 및 TCP/IP 주소에 대 한 DNS 항목][sap-ha-guide-figure-6004]

DNS 항목을 만드는 hello 절차도 주 hello에 자세히 설명 되어 [Windows Vm에서 SAP NetWeaver 고가용성에 대 한 가이드][sap-ha-guide-9.1.1]합니다.

> [!NOTE]
> hello hello 추가 ASCS/SCS 인스턴스의 toohello 가상 호스트 이름이 할당 하는 새 IP 주소 해야 수 hello hello toohello SAP Azure 부하 분산 장치를 할당 하는 새 IP 주소와 동일 합니다.
>
>이 시나리오에서 hello IP 주소가 10.0.0.50 되었습니다.

### <a name="add-an-ip-address-tooan-existing-azure-internal-load-balancer-by-using-powershell"></a>PowerShell을 사용 하 여에서 IP 주소 tooan 기존 Azure 내부 부하 분산 장치 추가

SAP ASCS/SCS 인스턴스가 둘 이상 toocreate hello 동일한 WSFC 클러스터의 경우 기존 Azure 내부 부하 분산 장치는 IP 주소 tooan tooadd PowerShell을 사용 합니다. 각 IP 주소에는 고유한 부하 분산 규칙, 프로브 포트, 프런트 엔드 IP 풀 및 백 엔드 풀이 필요합니다.

hello 다음 스크립트 추가 새 IP 주소 tooan 기존 부하 분산 장치입니다. 사용자 환경에 대 한 hello PowerShell 변수를 업데이트 합니다. hello 스크립트는 모든 SAP ASCS/SCS 포트에 대 한 모든 필요한 부하 분산 규칙을 만듭니다.

```powershell

# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>
Clear-Host
$ResourceGroupName = "SAP-MULTI-SID-Landscape"      # Existing resource group name
$VNetName = "pr2-vnet"                        # Existing virtual network name
$SubnetName = "Subnet"                        # Existing subnet name
$ILBName = "pr2-lb-ascs"                      # Existing ILB name                      
$ILBIP = "10.0.0.50"                          # New IP address
$VMNames = "pr2-ascs-0","pr2-ascs-1"          # Existing cluster virtual machine names
$SAPInstanceNumber = 50                       # SAP ASCS/SCS instance number: must be a unique value for each cluster
[int]$ProbePort = "623$SAPInstanceNumber"     # Probe port: must be a unique value for each IP and load balancer

$ILB = Get-AzureRmLoadBalancer -Name $ILBName -ResourceGroupName $ResourceGroupName

$count = $ILB.FrontendIpConfigurations.Count + 1
$FrontEndConfigurationName ="lbFrontendASCS$count"
$LBProbeName = "lbProbeASCS$count"

# Get hello Azure VNet and subnet
$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName
$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName

# Add second front-end and probe configuration
Write-Host "Adding new front end IP Pool '$FrontEndConfigurationName' ..." -ForegroundColor Green
$ILB | Add-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.Id
$ILB | Add-AzureRmLoadBalancerProbeConfig -Name $LBProbeName  -Protocol Tcp -Port $Probeport -ProbeCount 2 -IntervalInSeconds 10  | Set-AzureRmLoadBalancer

# Get new updated configuration
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName
# Get new updated LP FrontendIP COnfig
$FEConfig = Get-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB
$HealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

# Add new back-end configuration into existing ILB
$BackEndConfigurationName  = "backendPoolASCS$count"
Write-Host "Adding new backend Pool '$BackEndConfigurationName' ..." -ForegroundColor Green
$BEConfig = Add-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB | Set-AzureRmLoadBalancer

# Get new updated config
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName

# Assign VM NICs toobackend pool
$BEPool = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB
foreach($VMName in $VMNames){
        $VM = Get-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VMName
        $NICName = ($VM.NetworkInterfaceIDs[0].Split('/') | select -last 1)        
        $NIC = Get-AzureRmNetworkInterface -name $NICName -ResourceGroupName $ResourceGroupName                
        $NIC.IpConfigurations[0].LoadBalancerBackendAddressPools += $BEPool
        Write-Host "Assigning network card '$NICName' of hello '$VMName' VM toohello backend pool '$BackEndConfigurationName' ..." -ForegroundColor Green
        Set-AzureRmNetworkInterface -NetworkInterface $NIC
        #start-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VM.Name
}


# Create load-balancing rules
$Ports = "445","32$SAPInstanceNumber","33$SAPInstanceNumber","36$SAPInstanceNumber","39$SAPInstanceNumber","5985","81$SAPInstanceNumber","5$SAPInstanceNumber`13","5$SAPInstanceNumber`14","5$SAPInstanceNumber`16"
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName
$FEConfig = get-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB
$BEConfig = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB
$HealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

Write-Host "Creating load balancing rules for hello ports: '$Ports' ... " -ForegroundColor Green

foreach ($Port in $Ports) {

        $LBConfigrulename = "lbrule$Port" + "_$count"
        Write-Host "Creating load balancing rule '$LBConfigrulename' for hello port '$Port' ..." -ForegroundColor Green

        $ILB | Add-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig  -BackendAddressPool $BEConfig -Probe $HealthProbe -Protocol tcp -FrontendPort  $Port -BackendPort $Port -IdleTimeoutInMinutes 30 -LoadDistribution Default -EnableFloatingIP   
}

$ILB | Set-AzureRmLoadBalancer

Write-Host "Succesfully added new IP '$ILBIP' toohello internal load balancer '$ILBName'!" -ForegroundColor Green

```
Hello 스크립트를 실행 한 후 hello 스크린 샷 뒤에 표시 된 대로 Azure 포털을 hello hello에 결과가 표시 됩니다.

![Hello Azure 포털에서에서 새 프런트 엔드 IP 풀][sap-ha-guide-figure-6005]

### <a name="add-disks-toocluster-machines-and-configure-hello-sios-cluster-share-disk"></a>디스크 toocluster 컴퓨터를 추가 하 고 hello SIOS 클러스터 공유 디스크를 구성 합니다.

각 추가 SAP ASCS/SCS 인스턴스에 새 클러스터 공유 디스크를 추가해야 합니다. Windows Server 2012 r 2에서 현재 사용 중인 hello WSFC 클러스터 공유 디스크는 hello SIOS DataKeeper 소프트웨어 솔루션입니다.

다음 hello지 않습니다.
1. 더 추가 하의 디스크 또는 디스크 hello 같은 크기 (필요한 toostripe) tooeach hello의 클러스터 노드와 서식을 지정 합니다.
2. SIOS DataKeeper를 사용하여 저장소 복제를 구성합니다.

이 절차는 WSFC 클러스터 컴퓨터 hello에 SIOS DataKeeper를 이미 설치 있음을 가정 합니다. 설치 된 경우 이제 hello 컴퓨터 간의 복제를 구성 해야 합니다. hello 프로세스 주 hello에 자세히 설명 되어 [Windows Vm에서 SAP NetWeaver 고가용성에 대 한 가이드][sap-ha-guide-8.12.3.3]합니다.  

![Hello 새 SAP ASCS/SCS 공유 디스크에 대 한 미러링을 동기 DataKeeper][sap-ha-guide-figure-6006]

### <a name="deploy-vms-for-sap-application-servers-and-dbms-cluster"></a>SAP 응용 프로그램 서버 및 DBMS 클러스터에 대한 VM 배포

두 번째 SAP 시스템 hello에 대 한 toocomplete hello 인프라 준비 다음 hello지 않습니다.

1. SAP 응용 프로그램 서버에 대한 전용 VM을 배포하고 고유한 전용 가용성 그룹에 배치합니다.
2. DBMS 클러스터에 대한 전용 VM을 배포하고 고유한 전용 가용성 그룹에 배치합니다.


## <a name="install-hello-second-sap-sid2-netweaver-system"></a>Hello 두 번째 SID2의 SAP NetWeaver 시스템을 설치 합니다.

두 번째 SAP SID2 시스템 설치의 전체 과정 hello 주 hello에 설명 되어 [Windows Vm에서 SAP NetWeaver 고가용성에 대 한 가이드][sap-ha-guide-9]합니다.

hello 고급 절차는 다음과 같습니다.

1. [Hello SAP 첫 번째 클러스터 노드 설치][sap-ha-guide-9.1.2]합니다.  
 이 단계에서는 설치 하는 SAP hello의 가용성이 높은 ASCS/SCS 인스턴스에서 **기존 WSFC 클러스터 노드 1**합니다.

2. [Hello ASCS/SCS 인스턴스의 hello SAP 프로필 수정][sap-ha-guide-9.1.3]합니다.

3. [프로브 포트 구성][sap-ha-guide-9.1.4].  
 이 단계에서는 PowerShell을 사용하여 SAP 클러스터 리소스 SAP-SID2-IP 프로브 포트를 구성하고 있습니다. Hello SAP ASCS/SCS 클러스터 노드 중 하나에서이 구성을 실행 합니다.

4. [Hello 데이터베이스 인스턴스 설치] [sap-ha-가이드-9.2].  
 이 단계에서는 전용 WSFC 클러스터에 DBMS를 설치하고 있습니다.

5. [Hello 두 번째 클러스터 노드에 설치] [sap-ha-가이드-9.3].  
 이 단계에서는 hello 기존 WSFC 클러스터 노드 2의 가용성이 높은 ASCS/SCS 인스턴스에서 SAP을 설치 하는 합니다.

6. SAP ASCS/SCS 인스턴스와 ProbePort hello에 대 한 Windows 방화벽 포트를 엽니다.  
 SAP ASCS/SCS 인스턴스에 사용되는 두 클러스터 노드에서 SAP ASCS/SCS에서 사용하는 모든 Windows 방화벽 포트를 열고 있습니다. 이러한 포트는 hello에 나타나지 [Windows Vm에서 SAP NetWeaver 고가용성에 대 한 가이드][sap-ha-guide-8.8]합니다.  
 Hello Azure 내부 부하 분산 장치 프로브 포트에 62350 시나리오에서 열 수도 있습니다.

7. [Hello SAP 호출자 Windows 서비스 인스턴스의 hello 시작 유형을 변경][sap-ha-guide-9.4]합니다.

8. [Hello SAP 기본 응용 프로그램 서버 설치] [ sap-ha-guide-9.5] 새 hello에 VM 전용입니다.

9. [Hello SAP 추가 응용 프로그램 서버 설치] [ sap-ha-guide-9.6] 새 hello에 VM 전용입니다.

10. [테스트 hello SAP ASCS/SCS 인스턴스 장애 조치 및 SIOS 복제][sap-ha-guide-10]합니다.

## <a name="next-steps"></a>다음 단계

- [네트워킹 제한: Azure Resource Manager][networking-limits-azure-resource-manager]
- [Azure Load Balancer에 대한 다중 VIP][load-balancer-multivip-overview]
- [Windows VM에서 고가용성 SAP NetWeaver 가이드][sap-ha-guide]
