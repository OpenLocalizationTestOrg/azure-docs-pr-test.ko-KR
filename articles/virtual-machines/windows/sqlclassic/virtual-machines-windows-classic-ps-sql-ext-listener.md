---
title: "Always On 가용성 그룹에 대 한 외부 수신기 aaaConfigure | Microsoft Docs"
description: "이 자습서에서는의 공용 가상 IP 주소를 hello를 사용 하 여 외부에서 액세스할 수 있는 Azure에서 항상에 가용성 그룹 수신기를 만드는 단계 hello 연결 된 클라우드 서비스입니다."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a2453032-94ab-4775-b976-c74d24716728
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/31/2017
ms.author: mikeray
ms.openlocfilehash: f8e2110bcc25d9cb7653675cb4ae5c8d717b6902
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-external-listener-for-always-on-availability-groups-in-azure"></a>Azure에서 Always On 가용성 그룹에 대한 외부 수신기 구성
> [!div class="op_single_selector"]
> * [내부 수신기](../classic/ps-sql-int-listener.md)
> * [외부 수신기](../classic/ps-sql-ext-listener.md)
> 
> 

이 항목에서는 수신기는 Always On 가용성 그룹에서 외부에서 액세스할 수 있는를 tooconfigure 인터넷 hello 하는 방법입니다. 이 가능 hello 클라우드 서비스에 연결 하 여 **공용 VIP (가상 IP)** hello 수신기와 주소입니다.

> [!IMPORTANT] 
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../azure-resource-manager/resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.

가용성 그룹은 온-프레미스 전용, Azure 전용 또는 하이브리드 구성에 대한 온-프레미스와 Azure 모두에 걸쳐 있는 복제본을 포함할 수 있습니다. Azure 복제본 수 내에 있는 hello 동일한 지역 또는 여러 개의 가상 네트워크 (Vnet)를 사용 하 여 여러 지역에 걸쳐 있습니다. 다음 hello 단계 이미 있다고 가정 [가용성 그룹을 구성](../classic/portal-sql-alwayson-availability-groups.md) 했지만 수신기를 구성 하지 않은 합니다.

## <a name="guidelines-and-limitations-for-external-listeners"></a>외부 수신기에 대한 지침 및 제한 사항
Hello 클라우드 서비스 공용 VIP 주소를 사용 하 여 배포 하려는 경우 Azure의 hello 가용성 그룹 수신기에 대 한 지침을 따르는 참고 hello:

* hello 가용성 그룹 수신기는 Windows Server 2008 R2, Windows Server 2012 및 Windows Server 2012 r 2에서 지원 됩니다.
* hello 클라이언트 응용 프로그램은 가용성 그룹 Vm을 포함 하는 hello 보다 다른 클라우드 서비스에 있어야 합니다. 클라우드 서비스를 azure 직접 서버 반환 클라이언트와 서버 hello에 동일 하는 지원 하지 않습니다.
* 기본적으로이 문서의 단계 hello tooconfigure 하나의 수신기 toouse hello 서비스 VIP (가상 IP) 주소를 클라우드 하는 방법을 보여 줍니다. 그러나 가능한 tooreserve 되며 클라우드 서비스에 대 한 여러 VIP 주소를 만듭니다. 이렇게 하면 여러 수신기를 각각 다른 VIP와 연결 된이 문서 toocreate의 toouse hello 단계 있습니다. 여러 VIP 주소를 확인 하는 toocreate 방법에 대 한 내용은 [여러 vip가 클라우드 서비스 당](../../../load-balancer/load-balancer-multivip.md)합니다.
* Hello 온-프레미스 네트워크에 연결 toohello 있어야 하이브리드 환경에 대 한 수신기를 만드는 경우 추가 toohello에 공용 인터넷 hello Azure 가상 네트워크와 사이트 간 VPN. Hello Azure 서브넷에 있는 경우 hello 가용성 그룹 수신기는 hello hello 해당 클라우드 서비스의 공용 IP 주소를 통해서만 연결할 수 있습니다.
* 지원 되지 않으므로 동일한 클라우드 서비스를 사용 하는 내부 수신기 수도 있는 hello에 외부 수신기 toocreate hello 부하 분산 장치 ILB (내부)입니다.

## <a name="determine-hello-accessibility-of-hello-listener"></a>Hello 수신기의 hello 내게 필요한 옵션 확인
[!INCLUDE [ag-listener-accessibility](../../../../includes/virtual-machines-ag-listener-determine-accessibility.md)]

이 문서에서는 **외부 부하 분산**을 사용하는 수신기를 만드는 데 중점을 둡니다. 수신기는 tooyour 개인 가상 네트워크를 사용할 경우 참조를 설정 하기 위한 단계를 제공 하는이 문서의 hello 버전은 [ilb 수신기](../classic/ps-sql-int-listener.md)

## <a name="create-load-balanced-vm-endpoints-with-direct-server-return"></a>직접 서버 반환이 있는 부하 분산 VM 끝점 만들기
외부 부하 분산 Vm을 호스팅하는 hello 클라우드 서비스의 hello 가상 hello 공용 가상 IP 주소를 사용 합니다. 따라서 또는 하지 않는 toocreate 필요 합니다.이 경우 hello 부하 분산 장치를 구성 합니다.

Azure 복제본을 호스트하는 각 VM에 대해 부하가 분산된 끝점을 만들어야 합니다. 여러 지역에서 복제본이 있는 경우 각 복제본 마다 해당 지역 동일한 클라우드 서비스에 hello에 해야 hello 동일한 VNet입니다. 여러 Azure 지역에 걸쳐 있는 가용성 그룹 복제본을 만들려면 여러 VNet을 구성해야 합니다. VNet 간 연결 구성에 대 한 자세한 내용은 참조 하십시오. [VNet 구성 tooVNet 연결](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)합니다.

1. Azure 포털 hello tooeach hello 세부 정보 보기 및 복제본을 호스팅하는 VM을 이동 합니다.
2. Hello 클릭 **끝점** hello Vm 각각에 대해 탭 합니다.
3. 해당 hello 확인 **이름** 및 **공용 포트** hello 수신기 끝점의 원하는 toouse 이미 사용 중에서입니다. 아래 hello 예제에서 hello 이름은 "MyEndpoint"이 고 hello 포트는 "1433"입니다.
4. 로컬 클라이언트에서 다운로드 및 설치 [hello 최신 PowerShell 모듈](https://azure.microsoft.com/downloads/)합니다.
5. **Azure PowerShell**을 시작합니다. 새 PowerShell 세션이 열리고 Azure 관리 모듈이 로드 hello 합니다.
6. **Get-AzurePublishSettingsFile**을 실행합니다. 이 cmdlet tooa 브라우저 toodownload 게시 설정 파일 tooa 로컬 디렉터리를 안내합니다. Azure 구독에 대한 로그인 자격 증명을 묻는 메시지가 표시될 수 있습니다.
7. Hello 실행 **Import-azurepublishsettingsfile** hello의 hello 경로 사용 하 여 명령을 게시 설정 파일 다운로드:
   
        Import-AzurePublishSettingsFile -PublishSettingsFile <PublishSettingsFilePath>
   
    Hello 게시 되 면 설정 파일을 가져온 다음, hello PowerShell 세션에서 Azure 구독을 관리할 수 있습니다.
    
1. 아래의 hello PowerShell 스크립트를 텍스트 편집기에 복사 하 고 (기본값 제공 일부 매개 변수에 대 한) 사용자 환경 변수 값 toosuit hello를 설정 합니다. 가용성 그룹에 Azure 지역에 걸쳐 있는 경우 스크립트를 실행 해야 hello 한 번 hello 클라우드 서비스 및 해당 데이터 센터에 있는 노드에 대 한 각 데이터 센터에서 note 합니다.
   
        # Define variables
        $ServiceName = "<MyCloudService>" # hello name of hello cloud service that contains hello availability group nodes
        $AGNodes = "<VM1>","<VM2>","<VM3>" # all availability group nodes containing replicas in hello same cloud service, separated by commas
   
        # Configure a load balanced endpoint for each node in $AGNodes, with direct server return enabled
        ForEach ($node in $AGNodes)
        {
            Get-AzureVM -ServiceName $ServiceName -Name $node | Add-AzureEndpoint -Name "ListenerEndpoint" -Protocol "TCP" -PublicPort 1433 -LocalPort 1433 -LBSetName "ListenerEndpointLB" -ProbePort 59999 -ProbeProtocol "TCP" -DirectServerReturn $true | Update-AzureVM
        }

2. Hello 변수를 설정 하면 복사 hello 스크립팅해야 hello 텍스트 편집기에서 Azure PowerShell 세션 toorun에 있습니다. Hello 프롬프트에 여전히 표시 하는 경우 >>, enter 다시 toomake 있는지 hello 스크립트가 실행 되기 시작 합니다.

## <a name="verify-that-kb2854082-is-installed-if-necessary"></a>필요한 경우 KB2854082가 설치되었는지 확인합니다.
[!INCLUDE [kb2854082](../../../../includes/virtual-machines-ag-listener-kb2854082.md)]

## <a name="open-hello-firewall-ports-in-availability-group-nodes"></a>가용성 그룹 노드에서 방화벽 포트 열기 hello
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-open-firewall.md)]

## <a name="create-hello-availability-group-listener"></a>Hello 가용성 그룹 수신기 만들기

두 가지 단계로 hello 가용성 그룹 수신기를 만듭니다. 먼저 hello 클라이언트 액세스 지점 클러스터 리소스를 만들고 종속성을 구성 합니다. 둘째, powershell hello 클러스터 리소스를 구성 합니다.

### <a name="create-hello-client-access-point-and-configure-hello-cluster-dependencies"></a>Hello 클라이언트 액세스 지점을 만들고 hello 클러스터 종속성 구성
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-create-listener.md)]

### <a name="configure-hello-cluster-resources-in-powershell"></a>PowerShell에서 hello 클러스터 리소스를 구성 합니다.
1. 외부 부하 분산에 대 한 hello 공용 가상 IP 주소 여 복제본이 포함 된 hello 클라우드 서비스의 가져와야 합니다. Azure 포털 hello에 로그인 합니다. 가용성 그룹 VM이 있는 toohello 클라우드 서비스를 이동 합니다. 열기 hello **대시보드** 보기.
2. 아래에 표시 된 hello 주소 **공용 VIP (가상 IP) 주소**합니다. 솔루션이 Vnet에 걸쳐 있으면 복제본을 호스팅하는 VM이 포함된 각 클라우드 서비스에 대해 이 단계를 반복합니다.
3. Hello Vm 중 하나에서 hello 아래의 PowerShell 스크립트를 텍스트 편집기에 복사 하 고 앞에서 기록해 둔 toohello 값 hello 변수를 설정 합니다.
   
        # Define variables
        $ClusterNetworkName = "<ClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP Address resource name
        $CloudServiceIP = "<X.X.X.X>" # Public Virtual IP (VIP) address of your cloud service
   
        Import-Module FailoverClusters
   
        # If you are using Windows Server 2012 or higher, use hello Get-Cluster Resource command. If you are using Windows Server 2008 R2, use hello cluster res command. Both commands are commented out. Choose hello one applicable tooyour environment and remove hello # at hello beginning of hello line tooconvert hello comment tooan executable line of code.
   
        # Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$CloudServiceIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"OverrideAddressMatch"=1;"EnableDhcp"=0}
        # cluster res $IPResourceName /priv enabledhcp=0 overrideaddressmatch=1 address=$CloudServiceIP probeport=59999  subnetmask=255.255.255.255
4. 한 번 hello 변수 설정, 관리자 권한 Windows PowerShell 창을 열고 hello 텍스트 편집기에서 hello 스크립트를 복사 했으며 Azure PowerShell 세션 toorun에 붙여 Hello 프롬프트에 여전히 표시 하는 경우 >>, enter 다시 toomake 있는지 hello 스크립트가 실행 되기 시작 합니다.
5. 각 VM에서 이 작업을 반복합니다. 이 스크립트는 hello 클라우드 서비스의 IP 주소로 hello hello IP 주소 리소스를 구성 하 고 hello 프로브 포트와 같은 다른 매개 변수를 설정 합니다. Hello IP 주소 리소스를 온라인 상태로 만들 때이 자습서의 앞부분에서 만든 hello 부하 분산 된 끝점에서 hello 프로브 포트에서 폴링 toohello를 응답할 수 있습니다.

## <a name="bring-hello-listener-online"></a>Hello 수신기를 온라인 상태로 전환
[!INCLUDE [Bring-Listener-Online](../../../../includes/virtual-machines-ag-listener-bring-online.md)]

## <a name="follow-up-items"></a>추가 작업 항목
[!INCLUDE [Follow-up](../../../../includes/virtual-machines-ag-listener-follow-up.md)]

## <a name="test-hello-availability-group-listener-within-hello-same-vnet"></a>Hello 가용성 그룹 수신기 테스트 (내 hello 동일한 VNet)
[!INCLUDE [Test-Listener-Within-VNET](../../../../includes/virtual-machines-ag-listener-test.md)]

## <a name="test-hello-availability-group-listener-over-hello-internet"></a>Hello 가용성 그룹 수신기 테스트 (을 통해 인터넷 hello)
외부 hello 가상 네트워크에서 순서 tooaccess hello 수신기에서 사용 해야 (이 항목에서 설명) 외부/공용 부하 분산 ILB hello 내 에서만 액세스할 수 있는 하는 대신 동일한 VNet입니다. Hello 연결 문자열에 hello 클라우드 서비스 이름을 지정합니다. 예를 들어, hello 이름의 클라우드 서비스를 설치한 경우 *mycloudservice*, hello sqlcmd 문은 다음과 같이 됩니다.

    sqlcmd -S "mycloudservice.cloudapp.net,<EndpointPort>" -d "<DatabaseName>" -U "<LoginId>" -P "<Password>"  -Q "select @@servername, db_name()" -l 15

Hello 이전 예제와 달리 SQL 인증을 사용 해야, hello 호출자 hello를 통해 windows 인증을 사용할 수 없으므로 인터넷 합니다. 자세한 내용은 [Azure VM의 Always On 가용성 그룹: 클라이언트 연결 시나리오](http://blogs.msdn.com/b/sqlcat/archive/2014/02/03/alwayson-availability-group-in-windows-azure-vm-client-connectivity-scenarios.aspx)를 참조하세요. SQL 인증을 사용할 때는 확인 hello를 만들어 두 복제본에서 동일한 로그인 합니다. 가용성 그룹을 사용 하 여 로그인 문제를 해결 하는 방법에 대 한 자세한 내용은 참조 [어떻게 toomap 로그인 또는 사용 하 여에 포함 된 SQL 데이터베이스 사용자 tooconnect tooother 복제본 및 맵 tooavailability 데이터베이스가](http://blogs.msdn.com/b/alwaysonpro/archive/2014/02/19/how-to-map-logins-or-use-contained-sql-database-user-to-connect-to-other-replicas-and-map-to-availability-databases.aspx)합니다.

클라이언트를 지정 해야 하는 경우 hello Always On 복제본이 다른 서브넷에, **MultisubnetFailover = True** hello 연결 문자열에 있습니다. 따라서 hello 서로 다른 서브넷에 있는 병렬 연결 시도 tooreplicas 됩니다. 이 시나리오에는 영역 간 Always On 가용성 그룹 배포가 포함되어 있습니다.

## <a name="next-steps"></a>다음 단계
[!INCLUDE [Listener-Next-Steps](../../../../includes/virtual-machines-ag-listener-next-steps.md)]

