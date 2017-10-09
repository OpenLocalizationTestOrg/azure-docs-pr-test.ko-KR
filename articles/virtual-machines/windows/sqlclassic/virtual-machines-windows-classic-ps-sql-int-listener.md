---
title: "Azure에서 Always On 가용성 그룹에 대 한 ILB 수신기 aaaConfigure | Microsoft Docs"
description: "이 자습서에서는 hello 클래식 배포 모델을 사용 하 여 만든 리소스를 사용 하 고 Always On 가용성 그룹 수신기는 내부 부하 분산 장치를 사용 하 여 Azure에서 만듭니다."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 291288a0-740b-4cfa-af62-053218beba77
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/02/2017
ms.author: mikeray
ms.openlocfilehash: 2ce9b64fea491c945b58f7641e41fd39d90b078a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-ilb-listener-for-always-on-availability-groups-in-azure"></a>Azure에서 Always On 가용성 그룹에 대한 ILB 수신기 구성
> [!div class="op_single_selector"]
> * [내부 수신기](../classic/ps-sql-int-listener.md)
> * [외부 수신기](../classic/ps-sql-ext-listener.md)
>
>

## <a name="overview"></a>개요

> [!IMPORTANT]
> Azure에는 리소스를 만들고 작업하기 위한 두 가지 배포 모델, 즉 [Azure Resource Manager 및 클래식](../../../azure-resource-manager/resource-manager-deployment-model.md) 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델의 hello 사용을 설명합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.

hello 리소스 관리자 모델에서 Always On 가용성 그룹에 대 한 수신기 tooconfigure 참조 [Azure에서 Always On 가용성 그룹에 대 한 부하 분산 장치 구성](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md)합니다.

가용성 그룹은 온-프레미스 전용, Azure 전용 또는 하이브리드 구성에 대한 온-프레미스와 Azure 모두에 걸쳐 있는 복제본을 포함할 수 있습니다. Azure 복제본 수 내에 있는 hello 동일한 지역 또는 여러 개의 가상 네트워크를 사용 하는 여러 지역에 걸쳐 있습니다. hello이 문서의 절차 있다고 가정 이미 [가용성 그룹을 구성](../classic/portal-sql-alwayson-availability-groups.md) 했지만 아직 수신기를 구성 하지 않은 합니다.

## <a name="guidelines-and-limitations-for-internal-listeners"></a>내부 수신기에 대한 지침 및 제한 사항
hello를 사용 하 여 Azure에서 가용성 그룹 수신기로는 내부 부하 분산 장치 (ILB)의 지침에 따라 주체 toohello은입니다.

* hello 가용성 그룹 수신기는 Windows Server 2008 R2, Windows Server 2012 및 Windows Server 2012 r 2에서 지원 됩니다.
* Toohello ILB를 구성 하나만 내부 가용성 그룹 수신기는 hello 수신기 때문에 각 클라우드 서비스에 대해 지원 되 고 각 클라우드 서비스에 대 한 하나의 ILB 있습니다. 그러나 가능한 toocreate는 여러 외부 수신기입니다. 자세한 내용은 [Azure에서 Always On 가용성 그룹에 대한 외부 수신기 구성](../classic/ps-sql-ext-listener.md)을 참조하세요.

## <a name="determine-hello-accessibility-of-hello-listener"></a>Hello 수신기의 hello 내게 필요한 옵션 확인
[!INCLUDE [ag-listener-accessibility](../../../../includes/virtual-machines-ag-listener-determine-accessibility.md)]

이 문서에서는 ILB를 사용하는 수신기를 만드는 데 중점을 둡니다. 공용 또는 외부 수신기가 필요한 경우 구성 설정을 설명 하는이 문서의 hello 버전 참조는 [외부 수신기](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.

## <a name="create-load-balanced-vm-endpoints-with-direct-server-return"></a>직접 서버 반환이 있는 부하 분산 VM 끝점 만들기
먼저이 섹션의 뒷부분 hello 스크립트를 실행 하 여 받는 ILB를 만듭니다.

Azure 복제본을 호스트하는 각 VM에 대해 부하가 분산된 끝점을 만듭니다. 여러 지역에서 복제본이 있는 경우 각 복제본 마다 해당 지역 동일한 클라우드 서비스에 hello에 해야 hello 동일한 Azure 가상 네트워크입니다. 여러 Azure 지역에 걸쳐 있는 가용성 그룹 복제본을 만들려면 여러 가상 네트워크를 구성해야 합니다. 가상 네트워크 연결 크로스 구성 하는 방법에 대 한 자세한 내용은 참조 하십시오. [가상 네트워크 toovirtual 네트워크 연결을 구성](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)합니다.

1. Azure 포털 hello tooeach 복제본 tooview hello 세부 정보를 호스팅하는 VM을 이동 합니다.

2. Hello 클릭 **끝점** 각 VM에 대 한 탭 합니다.

3. 해당 hello 확인 **이름** 및 **공용 포트** toouse 이미 사용 중에서이 아니라 원하는 hello 수신기 끝점의 합니다. 이 섹션의 예제는 hello, hello name은 *MyEndpoint*, hello 포트는 *1433*합니다.

4. 로컬 클라이언트에서 다운로드 하 여 hello를 최신 버전 설치 [PowerShell 모듈](https://azure.microsoft.com/downloads/)합니다.

5. Azure PowerShell을 시작합니다.  
    새 PowerShell 세션이 열리고 hello Azure로 관리 모듈이 로드 합니다.

6. `Get-AzurePublishSettingsFile`을 실행합니다. 이 cmdlet tooa 브라우저 toodownload 게시 설정 파일 tooa 로컬 디렉터리를 안내합니다. Azure 구독에 대한 로그인 자격 증명을 묻는 메시지가 표시될 수 있습니다.

7. Hello 다음 실행 `Import-AzurePublishSettingsFile` hello의 hello 경로 사용 하 여 명령을 게시 설정 파일 다운로드:

        Import-AzurePublishSettingsFile -PublishSettingsFile <PublishSettingsFilePath>

    Hello 게시 설정 파일을 가져온 다음, hello PowerShell 세션에서 Azure 구독을 관리할 수 있습니다.

8. *ILB*에 대해 고정 IP 주소를 할당합니다. Hello 다음 명령을 실행 하 여 hello 현재 가상 네트워크 구성을 검토 합니다.

        (Get-AzureVNetConfig).XMLConfiguration
9. 참고 hello *서브넷* hello 복제본을 호스팅하는 hello Vm이 포함 된 hello 서브넷에 대 한 이름입니다. 이 이름은 hello 스크립트에서 $SubnetName hello 매개 변수에서 사용 됩니다.

10. 참고 hello *VirtualNetworkSite* 이름을 지정 하 고 시작 hello *AddressPrefix* hello 복제본을 호스팅하는 hello Vm이 포함 된 hello 서브넷에 대 한 합니다. 두 값 toohello 전달 하 여 사용 가능한 IP 주소에 대 한 확인 `Test-AzureStaticVNetIP` 명령이 고 hello를 검사 하 여 *AvailableAddresses*합니다. 예를 들어 hello 가상 네트워크 이름이 *MyVNet* 서브넷 주소 범위에서 시작 하 고 *172.16.0.128*, hello 다음 명령은 사용 가능한 주소가 나열 됩니다.

        (Test-AzureStaticVNetIP -VNetName "MyVNet"-IPAddress 172.16.0.128).AvailableAddresses
11. Hello 사용 가능한 주소 중 하나를 선택 하 고 hello 다음 단계에서 hello 스크립트의 hello $ILBStaticIP 매개 변수에서 사용할 키를 누릅니다.

12. 다음 PowerShell 스크립트 tooa 텍스트 편집기, hello 복사한 hello 변수 값 toosuit 환경을 설정 합니다. 일부 매개 변수에 대해 기본값이 제공되었습니다.  

    선호도 그룹을 사용하는 기존 배포는 ILB를 추가할 수 없습니다. ILB 요구 사항에 대한 자세한 내용은 [내부 부하 분산 장치 개요](../../../load-balancer/load-balancer-internal-overview.md)를 참조하세요.

    또한 가용성 그룹에 Azure 지역에 걸쳐 있는 경우 스크립트를 실행 해야 hello 한 번 hello 클라우드 서비스 및 해당 데이터 센터에 있는 노드에 대 한 각 데이터 센터에서.

        # Define variables
        $ServiceName = "<MyCloudService>" # hello name of hello cloud service that contains hello availability group nodes
        $AGNodes = "<VM1>","<VM2>","<VM3>" # all availability group nodes containing replicas in hello same cloud service, separated by commas
        $SubnetName = "<MySubnetName>" # subnet name that hello replicas use in hello virtual network
        $ILBStaticIP = "<MyILBStaticIPAddress>" # static IP address for hello ILB in hello subnet
        $ILBName = "AGListenerLB" # customize hello ILB name or use this default value

        # Create hello ILB
        Add-AzureInternalLoadBalancer -InternalLoadBalancerName $ILBName -SubnetName $SubnetName -ServiceName $ServiceName -StaticVNetIPAddress $ILBStaticIP

        # Configure a load-balanced endpoint for each node in $AGNodes by using ILB
        ForEach ($node in $AGNodes)
        {
            Get-AzureVM -ServiceName $ServiceName -Name $node | Add-AzureEndpoint -Name "ListenerEndpoint" -LBSetName "ListenerEndpointLB" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -InternalLoadBalancerName $ILBName -DirectServerReturn $true | Update-AzureVM
        }

13. Hello 변수를 설정 하면 복사 hello에서에서 스크립팅할 hello 텍스트 편집기 tooyour PowerShell 세션 toorun 것입니다. Hello 프롬프트에 여전히 표시 하는 경우  **>>** , enter 키를 다시 toomake 있는지 hello 스크립트 실행을 시작 합니다.

## <a name="verify-that-kb2854082-is-installed-if-necessary"></a>필요한 경우 KB2854082가 설치되었는지 확인합니다.
[!INCLUDE [kb2854082](../../../../includes/virtual-machines-ag-listener-kb2854082.md)]

## <a name="open-hello-firewall-ports-in-availability-group-nodes"></a>가용성 그룹 노드에서 방화벽 포트 열기 hello
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-open-firewall.md)]

## <a name="create-hello-availability-group-listener"></a>Hello 가용성 그룹 수신기 만들기

두 가지 단계로 hello 가용성 그룹 수신기를 만듭니다. 먼저 hello 클라이언트 액세스 지점 클러스터 리소스를 만들고 종속성을 구성 합니다. 둘째, powershell에서 hello 클러스터 리소스를 구성 합니다.

### <a name="create-hello-client-access-point-and-configure-hello-cluster-dependencies"></a>Hello 클라이언트 액세스 지점을 만들고 hello 클러스터 종속성 구성
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-create-listener.md)]

### <a name="configure-hello-cluster-resources-in-powershell"></a>PowerShell에서 hello 클러스터 리소스를 구성 합니다.
1. Ilb를 hello 앞에서 만든 ILB의 hello IP 주소를 사용 해야 합니다. PowerShell을 사용 하 여 hello 스크립트 다음에이 IP 주소를 tooobtain:

        # Define variables
        $ServiceName="<MyServiceName>" # hello name of hello cloud service that contains hello AG nodes
        (Get-AzureInternalLoadBalancer -ServiceName $ServiceName).IPAddress

2. Hello Vm 중 하나에 운영 체제 tooa 텍스트 편집기에 대 한 hello PowerShell 스크립트를 복사 하 고 앞에서 기록해 둔 toohello 값 hello 변수를 설정 합니다.

    Windows Server 2012 이상에서는 hello 다음 스크립트를 사용 합니다.

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}

    Windows Server 2008 r 2에 대 한 스크립트를 다음 hello를 사용 합니다.

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        cluster res $IPResourceName /priv enabledhcp=0 address=$ILBIP probeport=59999  subnetmask=255.255.255.255

3. 설정 hello 변수를 관리자 권한 Windows PowerShell 창을 열고을 설정한 후 붙여넣기 hello 스크립팅해야 hello 텍스트 편집기에서 PowerShell 세션 toorun에 있습니다. Hello 프롬프트에 여전히 표시 하는 경우  **>>** , Enter 키를 누릅니다 다시 toomake hello 스크립트 실행을 시작 하십시오.

4. Hello 각 VM에 대해 이전 단계를 반복 합니다.  
    이 스크립트는 hello 클라우드 서비스의 IP 주소로 hello hello IP 주소 리소스를 구성 하 고 hello 프로브 포트와 같은 다른 매개 변수를 설정 합니다. Hello IP 주소 리소스를 온라인 상태로 만들 때 앞에서 만든 hello 부하 분산 된 끝점에서 hello 프로브 포트에서 폴링 toohello를 응답할 수 있습니다.

## <a name="bring-hello-listener-online"></a>Hello 수신기를 온라인 상태로 전환
[!INCLUDE [Bring-Listener-Online](../../../../includes/virtual-machines-ag-listener-bring-online.md)]

## <a name="follow-up-items"></a>추가 작업 항목
[!INCLUDE [Follow-up](../../../../includes/virtual-machines-ag-listener-follow-up.md)]

## <a name="test-hello-availability-group-listener-within-hello-same-virtual-network"></a>Hello 가용성 그룹 수신기 테스트 (내 hello 동일한 가상 네트워크)
[!INCLUDE [Test-Listener-Within-VNET](../../../../includes/virtual-machines-ag-listener-test.md)]

## <a name="next-steps"></a>다음 단계
[!INCLUDE [Listener-Next-Steps](../../../../includes/virtual-machines-ag-listener-next-steps.md)]
