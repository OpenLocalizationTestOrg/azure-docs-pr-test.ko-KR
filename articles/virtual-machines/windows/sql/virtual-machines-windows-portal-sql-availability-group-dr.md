---
title: "서버 가용성 그룹-Azure 가상 컴퓨터-재해 복구 aaaSQL | Microsoft Docs"
description: "이 문서는 다른 지역에 복제 데이터베이스와 Azure 가상 컴퓨터에 SQL Server 가용성 tooconfigure 그룹화 하는 방법을 설명 합니다."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 388c464e-a16e-4c9d-a0d5-bb7cf5974689
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/02/2017
ms.author: mikeray
ms.openlocfilehash: df6238dc61c5a56879c75c9bf7314c618f43c0ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-always-on-availability-group-on-azure-virtual-machines-in-different-regions"></a>다른 하위 지역의 Azure Virtual Machines에서 Always On 가용성 그룹 구성

이 문서에서는 tooconfigure SQL Server Always On 가용성 복제본 원격 Azure 위치에 Azure 가상 컴퓨터에 그룹화 하는 방법을 설명 합니다. 이 구성 toosupport 재해 복구를 사용 합니다.

이 문서에는 리소스 관리자 모드에서 가상 컴퓨터 tooAzure 적용 됩니다.

hello 다음 이미지는 가용성 그룹의 일반적인 배포 Azure 가상 컴퓨터에

   ![가용성 그룹](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic.png)

이 배포에서 모든 가상 컴퓨터는 하나의 Azure 지역에 있습니다. hello 가용성 그룹 복제본이 동기 커밋 SQL-1과 2 SQL에서 자동 장애 조치를 가질 수 있습니다. toobuild이이 아키텍처 참조 [가용성 그룹 템플릿 또는 자습서](virtual-machines-windows-portal-sql-availability-group-overview.md)합니다.

이 아키텍처 취약 toodowntime 이면 hello Azure 지역에 액세스할 수 없게 됩니다. tooovercome이이 취약점 다른 Azure 지역에서 복제본을 추가 합니다. hello 다음 다이어그램 모양을 보여 줍니다 hello 새로운 아키텍처:

   ![가용성 그룹 DR](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic-dr.png)

hello 이전 다이어그램에서는 SQL 3 라는 새 가상 컴퓨터 SQL-3는 다른 Azure 지역에 있습니다. SQL 3 toohello Windows Server 장애 조치 클러스터에 추가 됩니다. SQL-3는 가용성 그룹 복제본을 호스트할 수 있습니다. 마지막으로, 해당 hello SQL 3에 대 한 Azure 지역에 새 Azure 부하 분산 장치를 확인 합니다.

>[!NOTE]
> Azure 가용성 집합은 동일한 지역 hello 가상 컴퓨터가 하나 이상 필요 합니다. 경우에 하나의 가상 컴퓨터에 hello 지역에 있으면 hello 가용성 집합에 필요 하지 않습니다. 생성 시 가용성 집합에 하나의 가상 컴퓨터만 배치할 수 있습니다. Hello 가상 컴퓨터 가용성 집합에 이미 있으면 추가 나중에 복제본 가상 컴퓨터를 추가할 수 있습니다.

이 아키텍처에서 비동기 커밋 가용성 모드와 수동 장애 조치 모드 hello 원격 영역의 hello 복제본 일반적으로 구성 됩니다.

가용성 그룹 복제본이 다른 Azure 지역의 Azure Virtual Machines에 있는 경우에 각 지역에 다음이 필요합니다.

* 가상 네트워크 게이트웨이
* 가상 네트워크 게이트웨이 연결

hello 다음 다이어그램에서는 데이터 센터 간에 hello 네트워크 통신 하는 방법을

   ![가용성 그룹](./media/virtual-machines-windows-portal-sql-availability-group-dr/01-vpngateway-example.png)

>[!IMPORTANT]
>이 아키텍처에서는 Azure 지역 간에 복제되는 데이터에 대해 아웃바운드 데이터 요금이 부과됩니다. [대역폭 가격 책정](http://azure.microsoft.com/pricing/details/bandwidth/)을 참조하세요.  

## <a name="create-remote-replica"></a>원격 복제본 만들기

다음 단계는 원격 데이터 센터로의 복제 toocreate hello지 않습니다.

1. [Hello 새 영역에서 가상 네트워크 만들기](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md)합니다.

1. [Hello Azure 포털을 사용 하 여 VNet 대 VNet 연결 구성](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)합니다.

   >[!NOTE]
   >경우에 따라 toouse PowerShell toocreate hello VNet 대 VNet 연결을 할 수 있습니다. 예를 들어 서로 다른 Azure 계정을 사용 하는 경우 hello 연결 hello 포털에서 구성할 수 없습니다. 이 경우 참조 [Azure 포털 hello 사용 하 여 구성 VNet 대 VNet 연결](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)합니다.

1. [Hello 새 영역에서 도메인 컨트롤러 만들기](../../../active-directory/active-directory-new-forest-virtual-machine.md)합니다.

   이 도메인 컨트롤러는 hello 기본 사이트의 hello 도메인 컨트롤러를 사용할 수 없는 경우 인증을 제공 합니다.

1. [Hello 새 영역에는 SQL Server 가상 컴퓨터를 만들](virtual-machines-windows-portal-sql-server-provision.md)합니다.

1. [Hello 새 영역에 hello 네트워크에는 Azure 부하 분산 장치를 만듭니다](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer)합니다.

   이 부하 분산 장치는 다음 조건을 충족해야 합니다.

   - 에 새 가상 컴퓨터를 hello 처럼 동일한 네트워크 및 서브넷 hello 합니다.
   - Hello 가용성 그룹 수신기에 대 한 고정 IP 주소를 있어야 합니다.
   - Hello 가상 컴퓨터 부하 분산 장치 hello으로 같은 지역 hello만 이루어진 백 엔드 풀을 포함 합니다.
   - TCP 포트 프로브 toohello 특정 IP 주소를 사용 합니다.
   - 부하 분산 규칙 특정 toohello hello에서 만든 SQL Server가 동일한 지역입니다.  

1. [장애 조치 클러스터링 기능 toohello 추가 새 SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms)합니다.

1. [Hello 새 SQL Server toohello 도메인 가입](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain)합니다.

1. [도메인 계정 hello 새 SQL Server 서비스 계정 toouse 설정](virtual-machines-windows-portal-sql-availability-group-prereq.md#setServiceAccount)합니다.

1. [Hello 새 SQL Server toohello Windows Server 장애 조치 클러스터를 추가](virtual-machines-windows-portal-sql-availability-group-tutorial.md#addNode)합니다.

1. Hello 클러스터 IP 주소 리소스를 만듭니다.

   장애 조치 클러스터 관리자에서 hello IP 주소 리소스를 만들 수 있습니다. Hello 가용성 그룹 역할을 마우스 오른쪽 단추로 클릭 하 여, **리소스 추가**, **더 리소스**를 클릭 하 고 **IP 주소**합니다.

   ![IP 주소 만들기](./media/virtual-machines-windows-portal-sql-availability-group-dr/20-add-ip-resource.png)

   이 IP 주소를 다음과 같이 구성합니다.

   - Hello 네트워크를 사용 하 여 hello 원격 데이터 센터에서.
   - Hello 새 Azure 부하 분산 장치에서 hello IP 주소를 할당 합니다. 

1. 새 SQL Server SQL Server 구성 관리자에서 hello [Always On 가용성 그룹을 사용 하도록 설정](http://msdn.microsoft.com/library/ff878259.aspx)합니다.

1. [열기 방화벽 포트를 새 SQL Server hello](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall)합니다.

   tooopen 필요한 hello 포트 번호는 사용자 환경에 따라 달라 집니다. 열린 포트 미러링 끝점 및 Azure hello에 대 한 부하 분산 장치 상태 프로브 합니다.

1. [Hello에 복제본 toohello 가용성 그룹을 추가 새 SQL Server](http://msdn.microsoft.com/library/hh213239.aspx)합니다.

   원격 Azure 지역에 있는 복제본의 경우 수동 장애 조치를 사용한 비동기 복제에 대해 설정합니다.  

1. Hello 수신기 클라이언트 액세스 지점 (네트워크 이름) 클러스터에 대 한 종속성으로 hello IP 주소 리소스를 추가 합니다.

   hello 다음 스크린샷은 올바르게 구성 된 IP 주소 클러스터 리소스:

   ![가용성 그룹](./media/virtual-machines-windows-portal-sql-availability-group-dr/50-configure-dependency-multiple-ip.png)

   >[!IMPORTANT]
   >hello 클러스터 리소스 그룹에는 IP 주소가 모두 포함 되어 있습니다. IP 주소는 hello 수신기 클라이언트 액세스 지점에 대 한 종속성입니다. 사용 하 여 hello **또는** hello 클러스터 종속성 구성의 연산자입니다.

1. [PowerShell에서 hello 클러스터 매개 변수를 설정](virtual-machines-windows-portal-sql-availability-group-tutorial.md#setparam)합니다.

새 영역 hello hello 부하 분산 장치에 구성 된 프로브 포트 hello 클러스터 네트워크 이름, IP 주소와 hello PowerShell 스크립트를 실행 합니다.

   ```PowerShell
   $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster name for hello network in hello new region (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name).
   $IPResourceName = "<IPResourceName>" # hello cluster name for hello new IP Address resource.
   $ILBIP = “<n.n.n.n>” # hello IP Address of hello Internal Load Balancer (ILB) in hello new region. This is hello static IP address for hello load balancer you configured in hello Azure portal.
   [int]$ProbePort = <nnnnn> # hello probe port you set on hello ILB.

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```

## <a name="set-connection-for-multiple-subnets"></a>여러 서브넷에 대한 연결 설정

hello 원격 데이터 센터에 hello 복제본 hello 가용성 그룹의 일부 이지만 다른 서브넷에. 이 복제본이 주 복제본 hello, 응용 프로그램 연결 제한 시간이 발생할 수 있습니다. 이 동작은 온-프레미스 가용성 그룹 다중 서브넷 배포에서와 동일 hello 됩니다. 클라이언트 응용 프로그램에서 tooallow 연결은 hello 클라이언트 연결을 업데이트 하거나 hello 클러스터 네트워크 이름 리소스에 대 한 캐싱을 이름 확인을 구성 합니다.

가급적 hello 클라이언트 연결 문자열 tooset 업데이트 `MultiSubnetFailover=Yes`합니다. [MultiSubnetFailover로 연결](http://msdn.microsoft.com/library/gg471494#Anchor_0)을 참조하세요.

연결 문자열 hello를 수정할 수 없는 경우 이름 확인 캐싱을 구성할 수 있습니다. [다중 서브넷 가용성 그룹의 연결 시간 제한](http://blogs.msdn.microsoft.com/alwaysonpro/2014/06/03/connection-timeouts-in-multi-subnet-availability-group/)을 참조하세요.

## <a name="fail-over-tooremote-region"></a>장애 조치 tooremote 영역

tootest 수신기 연결 toohello 원격 영역 hello 복제본 toohello 원격 지역의 실패할 수 있습니다. Hello 복제본이 비동기 인 동안 장애 조치가 취약 toopotential 데이터가 손실 됩니다. 데이터 손실 없이 통해 toofail hello 가용성 모드 toosynchronous 변경 하 고 장애 조치 모드 tooautomatic hello를 설정 합니다. 단계를 수행 하는 hello를 사용 합니다.

1. **개체 탐색기**, toohello hello 주 복제본을 호스팅하는 SQL Server 인스턴스에 연결 합니다.
1. **Always On 가용성 그룹**, **가용성 그룹** 아래에서 가용성 그룹을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.
1. Hello에 **일반** 페이지의 **가용성 복제본**, 집합 hello hello DR 사이트 toouse의 보조 복제본 **동기 커밋** 가용성 모드와 **자동** 장애 조치 모드입니다.
1. 보조 복제본을 고가용성에 대 한 기본 복제 데이터베이스와 같은 사이트에 있을 경우이 복제본에 너무 설정**비동기 커밋** 및 **수동**합니다.
1. 확인을 클릭합니다.
1. **개체 탐색기**hello 가용성 그룹을 마우스 오른쪽 단추로 클릭 하 고 클릭 **대시보드 표시**합니다.
1. Hello 대시보드에서 해당 hello 확인 hello DR 사이트에서 복제본이 동기화 합니다.
1. **개체 탐색기**hello 가용성 그룹을 마우스 오른쪽 단추로 클릭 하 고 클릭 **장애 조치 중...** . SQL Server Management Studio를 통해 SQL Server 마법사 toofail을 열립니다.  
1. 클릭 **다음**, 및 hello DR 사이트에서 SQL Server 인스턴스 선택 hello 합니다. 다시 **다음**을 클릭합니다.
1. Hello DR 사이트에서 toohello SQL Server 인스턴스에 연결 하 고 클릭 **다음**합니다.
1. Hello에 **요약** 페이지 hello 설정을 확인 하 고 클릭 **마침**합니다.

연결 테스트를 마친 후 hello 주 복제본 백 tooyour 주 데이터 센터 및 설정을 hello 가용성 모드 백 tootheir 정상 작동을 이동 합니다. hello 아래 표에 나와 hello이이 문서에서 설명 하는 hello 아키텍처에 대 한 기본 작업 설정.

| 위치 | 서버 인스턴스 | 역할 | 가용성 모드 | 장애 조치(Failover) 모드
| ----- | ----- | ----- | ----- | -----
| 주 데이터 센터 | SQL-1 | 보조 | 동기 | 자동
| 주 데이터 센터 | SQL-2 | 주 | 동기 | 자동
| 보조 또는 원격 데이터 센터 | SQL-3 | 주 | 비동기 | 설명서


### <a name="more-information-about-planned-and-forced-manual-failover"></a>계획된 및 강제 수동 장애 조치에 대한 자세한 내용

자세한 내용은 hello 다음 항목을 참조 하세요.

- [가용성 그룹의 계획된 수동 장애 조치 수행(SQL Server)](http://msdn.microsoft.com/library/hh231018.aspx)
- [가용성 그룹의 강제 수동 장애 조치 수행(SQL Server)](http://msdn.microsoft.com/library/ff877957.aspx)

## <a name="additional-links"></a>추가 링크

* [Always On 가용성 그룹](http://msdn.microsoft.com/library/hh510230.aspx)
* [Azure 가상 컴퓨터](http://docs.microsoft.com/azure/virtual-machines/windows/)
* [Azure Load Balancer](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer)
* [Azure 가용성 집합](../manage-availability.md)
