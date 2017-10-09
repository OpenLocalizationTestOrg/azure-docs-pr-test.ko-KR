---
title: "aaaHigh 고가용성 및 재해 복구 SQL Server에 대 한 | Microsoft Docs"
description: "자세한 내용은 Azure 가상 컴퓨터에서 실행 중인 SQL Server에 대 한 다양 한 유형의 HADR 전략 hello 합니다."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 53981f7e-8370-4979-b26a-93a5988d905f
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/27/2017
ms.author: mikeray
ms.openlocfilehash: 2b62d8b30520952ba6b7da7177a2c2de95bea8ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-and-disaster-recovery-for-sql-server-in-azure-virtual-machines"></a>Azure 가상 컴퓨터의 SQL Server에 대한 고가용성 및 재해 복구

SQL Server와 함께 Microsoft Azure 가상 컴퓨터 (Vm)는 고가용성 및 재해 복구 (HADR) 데이터베이스 솔루션 hello 비용을 절감 시킬 수 있습니다. 대부분의 SQL Server HADR 솔루션은 Azure 가상 컴퓨터에서 지원됩니다. Azure 전용으로도, 하이브리드 솔루션으로도 사용 가능합니다. Azure 전용 솔루션에서는 hello 전체 HADR 시스템은 Azure에서 실행 됩니다. 하이브리드 구성 hello 솔루션의 일부가 Azure에서 실행 되며 다른 파트 실행 온-프레미스 조직에서 hello 합니다. hello hello Azure 환경의 유연성을 사용 하면 toomove 부분적으로 또는 완전히 tooAzure toosatisfy hello 예산과 HADR 요구 사항을 SQL server 데이터베이스 시스템입니다.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="understanding-hello-need-for-an-hadr-solution"></a>HADR 솔루션에 대 한 이해 hello 필요
가 tooyou tooensure 데이터베이스 시스템에 있는지 hello 서비스 수준 계약 (SLA) 요구 하는 hello HADR 기능입니다. Azure 서비스 복구 클라우드 서비스 및 가상 컴퓨터에 대 한 오류 복구 검색과 같은 고가용성 메커니즘을 제공 하는 hello 팩트 자체 못하고 hello 원하는 SLA를 충족할 수 있습니다. 이러한 메커니즘 hello Vm의 고가용성 hello 하지만 높은 가용성 hello Vm 내에서 실행 되는 SQL Server의 hello 보호 합니다. Hello VM 온라인 상태이 고 정상 상태일 것에 대 한 SQL Server 인스턴스 toofail hello 가능 합니다. Azure에서 제공 하는 고가용성 메커니즘에도 hello hello Vm의 작동 중단 시간에 대 한 허용 되는 또한 due tooevents 같은 소프트웨어 또는 하드웨어 오류 및 운영 체제 업그레이드를 복구 합니다.

지역 복제라는 기능으로 구현되는 Azure의 GRS(지역 중복 저장)도 데이터베이스의 적절한 재해 복구 솔루션이 되지 못할 수 있습니다. 지리적 복제에서 데이터를 비동기적으로 보내기 때문에 대 한 최근 업데이트로 재해의 hello 이벤트에서 손실 될 수 있습니다. 지리적 복제 제한과 관련 된 자세한 내용은 hello에 대해서는 설명 [지리적 복제가 각기 다른 디스크에 데이터 및 로그 파일에 대 한 지원 되지 않음](#geo-replication-support) 섹션.

## <a name="hadr-deployment-architectures"></a>HADR 배포 아키텍처
Azure에서 지원하는 SQL Server HADR 기술은 다음과 같습니다.

* [Always On 가용성 그룹](https://technet.microsoft.com/library/hh510230.aspx)
* [Always On 장애 조치 클러스터 인스턴스](https://technet.microsoft.com/library/ms189134.aspx)
* [로그 전달](https://technet.microsoft.com/library/ms187103.aspx)
* [Azure Blob Storage 서비스로 SQL Server 백업 및 복원](https://msdn.microsoft.com/library/jj919148.aspx)
* [데이터베이스 미러링](https://technet.microsoft.com/library/ms189852.aspx) - SQL Server 2016에서에서 사용되지 않음

가능한 toocombine hello 기술을 함께 tooimplement 고가용성 및 재해 복구 기능이 둘 다 있는 SQL Server 솔루션은 사용 하는 hello 기술에 따라 하이브리드 배포 hello Azure 가상 네트워크로 VPN 터널이 필요할 수 있습니다. 아래 섹션에서는 hello 알려주는 hello 예제 배포 아키텍처의 일부입니다.

## <a name="azure-only-high-availability-solutions"></a>Azure 전용: 고가용성 솔루션

가용성 그룹이라고 하는 Always On 가용성 그룹을 사용하여 데이터베이스 수준에서 SQL Server에 대한 고가용성 솔루션을 유지할 수 있습니다. 장애 조치 클러스터 인스턴스라고 하는 Always On 장애 조치 클러스터 인스턴스를 사용하여 인스턴스 수준에서 고가용성 솔루션을 만들 수도 있습니다. 추가적인 중복의 경우 장애 조치 클러스터 인스턴스에서 가용성 그룹을 만들어 두 수준 모두에서 중복을 만들 수 있습니다. 

| 기술 | 아키텍처의 예 |
| --- | --- |
| **가용성 그룹** |가용성 복제본에서 Azure Vm에서 실행 hello 동일 지역 고가용성을 제공 합니다. Windows 장애 조치 클러스터링에 Active Directory 도메인이 필요 하기 때문에 VM 도메인 컨트롤러 tooconfigure를 해야 합니다.<br/> ![가용성 그룹](./media/virtual-machines-windows-sql-high-availability-dr/azure_only_ha_always_on.gif)<br/>자세한 내용은 [Azure에서 가용성 그룹 구성(GUI)](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)을 참조하세요. |
| **장애 조치 클러스터 인스턴스** |공유 저장소가 필요한 FCI(장애 조치 클러스터 인스턴스)는 3가지 방법으로 만들 수 있습니다.<br/><br/>1. 연결 된 스토리지를 사용 하 여 Azure Vm에서 실행 하는 2 노드 장애 조치 클러스터 [Windows Server 2016 저장소 공간 다이렉트 \(S2D\) ](virtual-machines-windows-portal-sql-create-failover-cluster.md) tooprovide 소프트웨어 기반 가상 SAN.<br/><br/>2. 타사 클러스터링 솔루션에서 지원하는 저장소를 사용하여 Azure VM에서 실행되는 2노드 장애 조치 클러스터입니다. SIOS DataKeeper를 사용하는 특정 예제는 [장애 조치 클러스터링 및 타사 소프트웨어 SIOS DataKeeper를 사용하는 파일 공유에 대한 고가용성](https://azure.microsoft.com/blog/high-availability-for-a-file-share-using-wsfc-ilb-and-3rd-party-software-sios-datakeeper/)을 참조하세요.<br/><br/>3. ExpressRoute를 통한 원격 iSCSI 대상 공유 블록 저장소를 사용하여 Azure VM에서 실행되는 2노드 장애 조치 클러스터입니다. 예를 들어 NetApp 개인 저장소 (NPS) ExpressRoute 통해 iSCSI 대상 Equinix tooAzure Vm으로 노출합니다.<br/><br/>제 3 자 공유 저장소 및 데이터 복제 솔루션에 대 한 장애 조치에 있는 모든 문제 관련된 tooaccessing 데이터에 대 한 hello 공급 업체에 문의 해야.<br/><br/>이 솔루션은 프리미엄 저장소를 사용하지 않기 때문에 [Azure 파일 저장소](https://azure.microsoft.com/services/storage/files/) 맨 위에서 FCI를 사용하는 것은 아직 지원되지 않습니다. 노력 toosupport 곧이 있습니다. |

## <a name="azure-only-disaster-recovery-solutions"></a>Azure 전용: 재해 복구 솔루션
가용성 그룹, 데이터베이스 미러링을 사용하여 Azure 내의 SQL Server 데이터베이스에 대한 재해 복구 솔루션을 구축하거나 저장소 blob을 사용하여 백업 및 복원할 수 있습니다.

| 기술 | 아키텍처의 예 |
| --- | --- |
| **가용성 그룹** |재해 복구를 위해 가용성 복제본을 Azure VM의 여러 데이터 센터에서 실행합니다. 이렇게 여러 영역에 나누어 실행되는 솔루션은 완전한 사이트 중단이 발생해도 데이터를 보호할 수 있습니다. <br/> ![가용성 그룹](./media/virtual-machines-windows-sql-high-availability-dr/azure_only_dr_alwayson.png)<br/>있는 영역에서 모든 복제본은 동일한 클라우드 서비스와 동일한 VNet hello hello에서 이어야 합니다. 각 지역의 더 별도 VNet을 VNet tooVNet 연결 이러한 솔루션에 필요 합니다. 자세한 내용은 참조 [Azure 포털 hello 사용 하 여 구성 VNet 대 VNet 연결](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)합니다. 자세한 지침은 [다른 지역의 Azure Virtual Machines에서 SQL Server 가용성 그룹 구성](virtual-machines-windows-portal-sql-availability-group-dr.md)을 참조하세요.|
| **데이터베이스 미러링** |재해 복구를 위해 주 서버와 미러 서버를 다른 데이터 센터에서 실행합니다. Active Directory 도메인을 여러 데이터 센터에 사용할 수 없으므로 서버 인증서를 사용하여 배포해야 합니다.<br/>![데이터베이스 미러링](./media/virtual-machines-windows-sql-high-availability-dr/azure_only_dr_dbmirroring.gif) |
| **Azure Blob 저장소 서비스로 SQL Server 백업 및 복원** |프로덕션 데이터베이스가 재해 복구를 위해 다른 데이터 센터에서 직접 tooblob 저장소를 백업 합니다.<br/>![백업 및 복원](./media/virtual-machines-windows-sql-high-availability-dr/azure_only_dr_backup_restore.gif)<br/>자세한 내용은 [Azure 가상 컴퓨터에서 SQL Server의 백업 및 복원](virtual-machines-windows-sql-backup-recovery.md)을 참조하세요. |

## <a name="hybrid-it-disaster-recovery-solutions"></a>하이브리드 IT: 재해 복구 솔루션
가용성 그룹, 데이터베이스 미러링, 로그 전달을 사용하여 하이브리드 IT 환경 내에 SQL Server 데이터베이스에 대한 재해 복구 솔루션을 구축하고 Azure Blob 저장소를 사용하여 백업 및 복원할 수 있습니다.

| 기술 | 아키텍처의 예 |
| --- | --- |
| **가용성 그룹** |사이트간 재해 복구를 위해 일부 가용성 복제본은 Azure VM에서 실행되고 다른 복제본은 온-프레미스에서 실행됩니다. hello 프로덕션 사이트 수 온-프레미스 또는 Azure 데이터 센터에 있습니다.<br/>![가용성 그룹](./media/virtual-machines-windows-sql-high-availability-dr/hybrid_dr_alwayson.gif)<br/>모든 가용성 복제본에 있어야 하므로 hello 동일한 장애 조치 클러스터 hello 두 네트워크 모두 (다중 서브넷 장애 조치 클러스터)에 걸쳐 있어야 합니다. 이 구성은 Azure와 hello 온-프레미스 네트워크 간의 VPN 연결이 필요합니다.<br/><br/>데이터베이스의 성공적인 재해 복구를 위한도 hello 재해 복구 사이트에서 복제 도메인 컨트롤러를 설치 해야 합니다.<br/><br/>이 가능한 toouse hello SSMS tooadd는 Azure 복제본 tooan 기존 Always On 가용성 그룹에 복제본 추가 마법사입니다. 자세한 내용은 자습서를 참조 하십시오.: Always On 가용성 그룹 tooAzure를 확장 합니다. |
| **데이터베이스 미러링** |한 파트너가 Azure VM과 다른 hello에서 실행 중인 온-프레미스 서버 인증서를 사용 하 여 사이트 간 재해 복구를 위해 실행 합니다. 파트너에서 toobe 불필요 hello 동일한 Active Directory 도메인 및 VPN 연결이 필요 없습니다.<br/>![데이터베이스 미러링](./media/virtual-machines-windows-sql-high-availability-dr/hybrid_dr_dbmirroring.gif)<br/>다른 데이터베이스 미러링 시나리오 포함 한 파트너가 Azure VM에서 실행 하 고 hello 다른 실행에서에서 온-프레미스 hello 동일 사이트 간 재해 복구를 위해 Active Directory 도메인. A [hello Azure 가상 네트워크 및 hello 온-프레미스 네트워크 간의 VPN 연결이](../../../vpn-gateway/vpn-gateway-site-to-site-create.md) 가 필요 합니다.<br/><br/>데이터베이스의 성공적인 재해 복구를 위한도 hello 재해 복구 사이트에서 복제 도메인 컨트롤러를 설치 해야 합니다. |
| **로그 전달** |다른 hello 및 Azure VM에서 실행 하는 하나의 서버 온-프레미스 사이트 간 재해 복구를 위해 실행 합니다. 로그 전달 되므로 hello 및 hello Azure 가상 네트워크 간의 VPN 연결이 온-프레미스 네트워크는 필수 Windows 파일 공유에 따라 달라 집니다.<br/>![로그 전달](./media/virtual-machines-windows-sql-high-availability-dr/hybrid_dr_log_shipping.gif)<br/>데이터베이스의 성공적인 재해 복구를 위한도 hello 재해 복구 사이트에서 복제 도메인 컨트롤러를 설치 해야 합니다. |
| **Azure Blob 저장소 서비스로 SQL Server 백업 및 복원** |온-프레미스 프로덕션 데이터베이스가 재해 복구에 대 한 직접 tooAzure blob 저장소를 백업 합니다.<br/>![백업 및 복원](./media/virtual-machines-windows-sql-high-availability-dr/hybrid_dr_backup_restore.gif)<br/>자세한 내용은 [Azure 가상 컴퓨터에서 SQL Server의 백업 및 복원](virtual-machines-windows-sql-backup-recovery.md)을 참조하세요. |

## <a name="important-considerations-for-sql-server-hadr-in-azure"></a>Azure에서 SQL Server HADR에 대한 중요 고려 사항
Azure VM, 저장소 및 네트워킹은 온-프레미스, 가상화되지 않은 IT 인프라에서는 작동 특성이 달라집니다. Azure에서 SQL Server HADR 솔루션을 성공적으로 구현 하면 이러한 차이점을 이해 하려면 디자인 해야 솔루션 tooaccommodate 해당 합니다.

### <a name="high-availability-nodes-in-an-availability-set"></a>가용성 집합의 고가용성 노드
Azure에서 가용성 집합을 별도 오류 도메인 (Fd) 및 Ud (업데이트 도메인)에 tooplace hello 고가용성 노드를 사용 합니다. Azure Vm에 대 한 toobe에에서 배치 hello 동일한 가용성 집합에 배포 해야 hello에서 동일한 클라우드 서비스입니다. 동일한 클라우드 서비스에 참여할 수 hello의 노드만 동일한 가용성 집합을 hello 합니다. 자세한 내용은 참조 [가상 컴퓨터의 가용성 관리 hello](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

### <a name="failover-cluster-behavior-in-azure-networking"></a>Azure 네트워킹에서 장애 조치 클러스터의 동작
Azure에서 RFC 규격이 아닌 DHCP 서비스가 hello toohello 클러스터 네트워크 이름이 중복 IP 주소를 할당 되 고 인해 장애 조치 클러스터 구성 toofail 특정 hello 생성 될 수 있습니다, 그리고 hello 같은 hello 클러스터 노드 중 하 나와 같은 IP 주소입니다. Hello Windows 장애 조치 클러스터 기능에 따라 가용성 그룹을 구현 하는 경우에 문제입니다.

2-노드 클러스터를 만들고 온라인 상태로 만들 때 hello 시나리오를 고려해 보십시오.

1. hello 클러스터를 온라인 상태로 된 다음 NODE1 hello 클러스터 네트워크 이름에 대 한 동적으로 할당 된 IP 주소를 요청 합니다.
2. 1의 IP 주소가 아닌 IP 주소를 지정 하 여 hello DHCP 서비스 노드 1에서 해당 hello 요청 하는 hello DHCP 서비스를 인식 하므로 자체입니다.
3. Windows 중복 주소가 tooNODE1와 toohello 장애 조치 클러스터 네트워크 이름에 할당 된 hello 기본 클러스터 그룹 toocome 온라인 실패 감지 합니다.
4. hello 기본 클러스터 그룹 tooNODE2 hello 클러스터 IP 주소를 1의 IP 주소를 처리 하며 hello 기본 클러스터 그룹을 온라인 상태로 이동 합니다.
5. NODE2 tooestablish 1과 연결을 시도할 때 노드 1의 IP 주소 tooitself 확인 되므로 NODE1 향하는 패킷은 항상 NODE2 유지 합니다. NODE2 1과 연결을 설정할 수 없습니다, 다음 쿼럼을 잃고 hello 클러스터를 종료 합니다.
6. 그 동안 hello에 노드 1 패킷을 tooNODE2를 보낼 수는 있지만 NODE2 응답할 수 없습니다. NODE1 쿼럼을 잃고 hello 클러스터를 종료 합니다.

정적 IP 주소를 사용 하지 않는 169.254.1.1 같은 링크 로컬 IP 주소, 주문 toobring hello 클러스터 네트워크 이름 온라인에서 toohello 클러스터 네트워크 이름을 할당 하 여이 시나리오를 방지할 수 있습니다. toosimplify이 프로세스는, 참조 [가용성 그룹에 대 한 Azure에서 구성 하는 Windows 장애 조치 클러스터](http://social.technet.microsoft.com/wiki/contents/articles/14776.configuring-windows-failover-cluster-in-windows-azure-for-alwayson-availability-groups.aspx)합니다.

자세한 내용은 [Azure에서 가용성 그룹 구성(GUI)](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)을 참조하세요.

### <a name="availability-group-listener-support"></a>가용성 그룹 수신기 지원
가용성 그룹 수신기는 Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 및 Windows Server 2016에서 실행되는 Azure VM에서 지원됩니다. 이 지원은 hello 가용성 그룹 노드인 hello Azure Vm에서 사용 하도록 설정 하는 부하 분산 끝점을 사용 하 여 가능 합니다. Azure로 온-프레미스에서 실행 되는 클라이언트 응용 프로그램 모두에 대 한 수신기 toowork hello에 대 한 특수 구성 단계를 수행 해야 합니다.

수신기를 설정하는 두 가지 주요 옵션(외부(공용) 및 내부)이 있습니다. 인터넷 연결 부하 분산 장치 및 연결 된는 공용 VIP (가상 IP)를 통해 액세스할 수 있는 hello 외부 (공용) 수신기 사용 하 여 hello 인터넷 합니다. 내부 수신기는 내부 부하 분산 장치를 사용 하 여 및 동일한 가상 네트워크를 hello 내 클라이언트만 지원 합니다. 각 부하 분산 장치 유형에 대해 Direct Server Return (DSR)을 설정해야 합니다. 

Hello 클라이언트 연결 문자열을 포함 해야 hello 가용성 그룹 (예: Azure 영역을 교차 하는 배포) 여러 Azure 서브넷에 걸쳐 있는 경우 "**MultisubnetFailover = True**"입니다. 이 인해 hello 서로 다른 서브넷에 있는 병렬 연결 시도 toohello 복제본입니다. 수신기 설정에 대한 지침은 다음을 참조하세요.

* [Azure에서 가용성 그룹에 대한 ILB 수신기 구성](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md)
* [Azure에서 가용성 그룹에 대한 외부 수신기 구성](../classic/ps-sql-ext-listener.md)

여전히 tooeach 가용성 복제본 toohello 서비스 인스턴스에 직접 연결 하 여 개별적으로 연결할 수 있습니다. 또한 가용성 그룹이 데이터베이스 미러링 클라이언트와 호환 되므로 데이터베이스 hello 복제본이 구성 된 상태로 미러링 파트너 처럼 가용성 복제본 toohello 연결할 수 비슷한 toodatabase 미러링:

* 하나의 주 복제본과 하나의 보조 복제본
* hello 보조 복제본이 구성 되어 읽을 수 없는 같이 (**읽기용 보조 복제본** 옵션이 너무 설정**아니요**)

클라이언트 연결 문자열의 예 toothis 데이터베이스 미러링과 유사한 구성 ADO.NET 또는 SQL Server Native Client를 사용 하 여 해당 하는 다음과 같습니다.

    Data Source=ReplicaServer1;Failover Partner=ReplicaServer2;Initial Catalog=AvailabilityDatabase;

클라이언트 연결에 대한 자세한 내용은 다음을 참조하세요.

* [SQL Server Native Client와 연결 문자열 키워드 사용](https://msdn.microsoft.com/library/ms130822.aspx)
* [클라이언트 tooa 데이터베이스 미러링 세션 (SQL Server)를 연결 합니다.](https://technet.microsoft.com/library/ms175484.aspx)
* [TooAvailability 하이브리드 IT에서 그룹 수신기를 연결합니다.](http://blogs.msdn.com/b/sqlalwayson/archive/2013/02/14/connecting-to-availability-group-listener-in-hybrid-it.aspx)
* [가용성 그룹 수신기, 클라이언트 연결 및 응용 프로그램 장애 조치(failover)(SQL Server)](https://technet.microsoft.com/library/hh213417.aspx)
* [가용성 그룹과 데이터베이스 미러링 연결 문자열 사용](https://technet.microsoft.com/library/hh213417.aspx)

### <a name="network-latency-in-hybrid-it"></a>하이브리드 IT 환경의 네트워크 대기 시간
HADR 솔루션을 온-프레미스 네트워크와 Azure 간의 긴 네트워크 지연 시간 시간이 있을 수 있습니다 hello 가정 배포 해야 합니다. 복제본 tooAzure을 배포할 때는 hello 동기화 모드에 대 한 동기 커밋 대신 비동기 커밋을 사용 해야 합니다. 경우 데이터베이스 미러링 서버를 배포 합니다. 온-프레미스와 Azure의 hello 보호 우선 모드 대신 hello 성능 우선 모드를 사용 합니다.

### <a name="geo-replication-support"></a>지역에서 복제 지원
Hello 데이터 파일과 로그 파일의 별도 디스크에 저장 된 같은 데이터베이스 toobe hello Azure 디스크의 지리적 복제를 지원 하지 않습니다. GRS는 변경 내용을 독립적이고 비동기적으로 각 디스크에 복제합니다. 이 메커니즘을 통해 hello 지리적으로 복제 된 복사본에서 하지만 여러 디스크의 지리적으로 복제 된 복사본 전체가 아닌 단일 디스크 내의 hello 쓰기 순서가 보장 합니다. 데이터 파일과 해당 로그 파일이 별도 디스크에 데이터베이스 toostore를 구성한 경우 hello를 복구할 디스크 재해 중단 되는 SQL Server의 미리 쓰기 로그 hello 및 ACID hello hello 로그 파일 보다 최신인 hello 데이터 파일의 복사본이 포함 될 수 있습니다. 트랜잭션의 속성입니다. Hello 저장소 계정에 hello 옵션 toodisable 지리적 복제 없는 경우 모든 데이터를 유지 해야 하 고 동일한 hello에서 지정된 된 데이터베이스에 대 한 로그 파일 디스크. Hello 데이터베이스의 크기 toohello 인해 둘 이상의 디스크를 사용 해야 할 경우 tooensure 데이터 중복 위에 나열 된 hello 재해 복구 솔루션 중 하나는 toodeploy를 해야 합니다.

## <a name="next-steps"></a>다음 단계
SQL Server와 Azure 가상 컴퓨터 toocreate 필요한 경우 참조 [Azure에서 SQL Server 가상 컴퓨터를 프로 비전](virtual-machines-windows-portal-sql-server-provision.md)합니다.

Azure VM에서 실행 중인 SQL Server에서 tooget hello 최상의 성능을에 hello 지침을 참조 하세요. [Azure 가상 컴퓨터의 SQL Server에 대 한 성능 모범 사례](virtual-machines-windows-sql-performance.md)합니다.

다른 항목은 서로 관련 toorunning Azure Vm에서 SQL Server에 대 한 참조 [Azure 가상 컴퓨터에 SQL Server](virtual-machines-windows-sql-server-iaas-overview.md)합니다.

### <a name="other-resources"></a>기타 리소스
* [Azure에 새 Active Directory 포리스트 설치](../../../active-directory/active-directory-new-forest-virtual-machine.md)
* [Azure VM에서 가용성 그룹을 위한 장애 조치 클러스터 만들기](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a)

