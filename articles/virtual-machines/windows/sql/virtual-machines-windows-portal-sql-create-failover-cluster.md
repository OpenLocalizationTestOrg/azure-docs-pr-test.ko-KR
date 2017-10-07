---
title: "aaaSQL 서버 FCI-Azure 가상 컴퓨터 | Microsoft Docs"
description: "이 문서에서는 설명 toocreate SQL Server 장애 조치 클러스터 인스턴스를 Azure 가상 컴퓨터는 방법입니다."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 9fc761b1-21ad-4d79-bebc-a2f094ec214d
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: bee3b27805c5f6cc02a43b25d480c129c254cb90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-sql-server-failover-cluster-instance-on-azure-virtual-machines"></a>Azure Virtual Machines에 SQL Server 장애 조치(Failover) 클러스터 인스턴스 구성

이 문서에 설명 방법을 toocreate SQL Server 장애 조치 클러스터 인스턴스 (FCI) 리소스 관리자 모델에서 Azure 가상 컴퓨터에 있습니다. 이 솔루션에서는 [저장소 공간 다이렉트 Windows Server 2016 Datacenter edition \(S2D\) ](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) hello 노드 (Azure Vm) 간에 hello 저장소 (데이터 디스크)를 동기화 하는 소프트웨어 기반 가상 SAN으로는 Windows 클러스터입니다. S2D는 Windows Server 2016의 새로운 기능입니다.

hello 다음 그림에 hello 완벽 한 솔루션 Azure 가상 컴퓨터에:

![가용성 그룹](./media/virtual-machines-windows-portal-sql-create-failover-cluster/00-sql-fci-s2d-complete-solution.png)

이전 다이어그램에 표시 하는 hello:

- Windows 장애 조치(Failover) 클러스터에 있는 두 개의 Azure Virtual Machines 가상 컴퓨터가 장애 조치 클러스터에 있는 경우 *클러스터 노드* 또는 *노드*라고도 합니다.
- 각 가상 컴퓨터에는 두 개 이상의 데이터 디스크가 있습니다.
- S2D는 hello 데이터 디스크에 hello 데이터를 동기화 하 고 저장소 풀으로 동기화 하는 hello 저장소를 제공 합니다.
- hello 저장소 풀에는 클러스터 공유 볼륨 (CSV) toohello 장애 조치 클러스터를 표시합니다.
- SQL Server FCI 클러스터 역할 hello hello 데이터 드라이브에 대 한 hello CSV를 사용합니다.
- Azure 부하 분산 장치 toohold hello IP 주소를 SQL Server FCI hello 합니다.
- Azure 가용성 집합 모든 hello 리소스를 보유합니다.

   >[!NOTE]
   >모든 Azure 리소스는 hello 다이어그램에서 hello에 동일한 리소스 그룹입니다.

S2D에 대한 자세한 내용은 [Windows Server 2016 Datacenter 버전 저장소 공간 다이렉트 \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)를 참조하세요.

S2D는 두 가지 유형의 아키텍처 수렴형 및 하이퍼 수렴형을 지원합니다. 이 문서에 hello 아키텍처 하이퍼 수렴 형는입니다. 하이퍼 수렴 형 인프라 위치 hello 저장소를 동일한 서버로 해당 호스트 클러스터 hello 응용 프로그램을 hello 합니다. 이 아키텍처에서 hello 저장소는 각 SQL Server FCI 노드에 있습니다.

### <a name="example-azure-template"></a>예제 Azure 템플릿

서식 파일에서 Azure의 hello 전체 솔루션을 만들 수 있습니다. 서식 파일의 예는 hello GitHub에서에서 사용할 수 있는 [Azure 빠른 시작 템플릿](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad)합니다. 이 예제는 특정 작업에 대해 설계되거나 테스트되지 않았습니다. S2D 저장소 연결 된 tooyour 도메인과 hello 템플릿 toocreate SQL Server FCI를 실행할 수 있습니다. Hello 서식 파일을 평가 하 고 용도 맞게 수정할 수 있습니다.

## <a name="before-you-begin"></a>시작하기 전에

몇 가지 방법으로 계속 진행 하기 전에 tooknow와 몇 가지 기능 필요한 위치에 필요 합니다.

### <a name="what-tooknow"></a>어떤 tooknow
다음 기술 hello 작동 이해가 있어야 합니다.

- [Windows 클러스터 기술](http://technet.microsoft.com/library/hh831579.aspx)
-  [SQL Server 장애 조치(Failover) 클러스터 인스턴스](http://msdn.microsoft.com/library/ms189134.aspx)

또한 다음 기술을 hello에 대 한 기본적인 지식이 있어야 합니다.

- [Windows Server 2016의 저장소 공간 다이렉트를 사용하는 하이퍼 수렴형 솔루션](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct)
- [Azure 리소스 그룹](../../../azure-resource-manager/resource-group-portal.md)

### <a name="what-toohave"></a>어떤 toohave

이 문서의 지침 hello를 수행 하기 전에 이미 있습니다.

- Microsoft Azure 구독
- Azure 가상 컴퓨터의 Windows 도메인
- Hello Azure 가상 컴퓨터의에서 toocreate 개체 사용 권한 있는 계정입니다.
- Azure 가상 네트워크와 서브넷에 다음과 같은 구성 요소가 hello에 대 한 충분 한 IP 주소 공간:
   - 두 가상 컴퓨터
   - hello 장애 조치 클러스터 IP 주소입니다.
   - 각 FCI에 대한 IP 주소
- DNS에 hello toohello 도메인 컨트롤러를 가리키는 Azure 네트워크를 구성 합니다.

이러한 필수 구성 요소가 준비되면 장애 조치 클러스터 빌드를 진행할 수 있습니다. hello 첫 번째 단계는 toocreate hello 가상 컴퓨터입니다.

## <a name="step-1-create-virtual-machines"></a>1단계: 가상 컴퓨터 만들기

1. Toohello 로그인 [Azure 포털](http://portal.azure.com) 를 구독 합니다.

1. [Azure 가용성 집합을 만듭니다](../tutorial-availability-sets.md).

   hello 가용성 오류 도메인 그룹 가상 컴퓨터를 설정 하 고 도메인을 업데이트 합니다. hello 가용성 집합을 사용 하면 응용 프로그램이 단일 hello 네트워크 스위치, 서버 랙의 전원 공급 장치 hello 등 실패 지점의 영향을 받지 않습니다.

   가상 컴퓨터에 대 한 hello 리소스 그룹을 만들지 않은 수행 Azure 가용성 집합을 만들 때. Hello Azure 포털 toocreate hello 가용성 집합을 사용 하는 경우 다음 단계 hello지 않습니다.

   - Hello Azure 포털에서에서 클릭 ** + ** tooopen hello Azure 마켓플레이스입니다. **가용성 집합**을 검색합니다.
   - **가용성 집합**을 클릭합니다.
   - **만들기**를 클릭합니다.
   - Hello에 **가용성 집합 만들기** 블레이드를 다음 값에는 집합 hello:
      - **이름**: hello 가용성 집합에 대 한 이름입니다.
      - **구독:** 사용자의 Azure 구독입니다.
      - **리소스 그룹**: 기존 그룹 toouse 클릭 **기존 항목 사용** 및 hello 드롭 다운 목록에서 선택 hello 그룹입니다. 그렇지 않은 경우 선택 **새로 만들기** hello 그룹에 대 한 이름을 입력 합니다.
      - **위치**: hello 위치 toocreate 설치할 가상 컴퓨터를 설정 합니다.
      - **오류 도메인**: hello 기본 (3)을 사용 합니다.
      - **업데이트 도메인**: hello 기본 (5)를 사용 합니다.
   - 클릭 **만들기** toocreate hello 가용성 집합입니다.

1. Hello 가용성 집합의 hello 가상 컴퓨터를 만듭니다.

   Hello Azure 가용성 집합에 두 개의 SQL Server 가상 컴퓨터를 프로 비전 합니다. 자세한 내용은 [hello Azure 포털에서에서 SQL Server 가상 컴퓨터를 프로 비전](virtual-machines-windows-portal-sql-server-provision.md)합니다.

   두 가상 컴퓨터를 다음에 배치합니다.

   - Hello 가능 여부를 설정 하는 같은 Azure 리소스 그룹에서는입니다.
   - Hello에 도메인 컨트롤러로 네트워크 동일 합니다.
   - 두 가상 컴퓨터에 대한 충분한 IP 주소 공간이 있는 서브넷 및 이 클러스터에서 사용할 수 있는 모든 FCI에.
   - Hello Azure 가용성 집합입니다.   

      >[!IMPORTANT]
      >가상 컴퓨터를 만든 후에 가용성 집합을 설정 또는 변경할 수 없습니다.

   Hello Azure Marketplace에서에서 이미지를 선택 합니다. 마켓플레이스를 사용할 수 있습니다 Windows Server 및 SQL Server 또는 Windows Server 정당한 hello를 사용 하 여 이미지를 포함 합니다. 자세한 내용은 [Azure Virtual Machines의 SQL Server 개요](../../virtual-machines-windows-sql-server-iaas-overview.md)를 참조하세요.

   hello 공식 SQL Server 이미지 hello Azure 갤러리에서에서 설치 된 SQL Server 인스턴스 및 hello SQL Server를 설치 하는 소프트웨어 및 hello 필요한 키를 포함 합니다.

   원하는 toohow toopay hello SQL Server 라이선스에 따라 hello 오른쪽 이미지를 선택 합니다.

   - **사용 라이선스 비용을 지불**: 이러한 이미지의 분당 비용 hello hello SQL Server 라이선스에 포함 됩니다.
      - **Windows Server Datacenter 2016의 SQL Server 2016 Enterprise**
      - **Windows Server Datacenter 2016의 SQL Server 2016 Standard**
      - **Windows Server Datacenter 2016의 SQL Server 2016 Developer**

   - **BYOL(사용자 라이선스 필요)**

      - **{BYOL} Windows Server Datacenter 2016의 SQL Server 2016 Enterprise**
      - **{BYOL} Windows Server Datacenter 2016의 SQL Server 2016 Standard**

   >[!IMPORTANT]
   >Hello 가상 컴퓨터를 만든 후 hello 사전 설치 된 독립 실행형 SQL Server 인스턴스를 제거 합니다. Hello 장애 조치 클러스터와 S2D을 구성한 후에 hello 사전 설치 된 SQL Server 미디어 toocreate hello SQL Server FCI를 사용 합니다.

   또는 바로 hello 운영 체제와 함께 Azure 마켓플레이스 이미지를 사용할 수 있습니다. 선택 된 **Windows Server 2016 Datacenter** 이미지 및 S2D 및 hello 장애 조치 클러스터 구성 후 hello SQL Server FCI를 설치 합니다. 이 이미지는 SQL Server 설치 이미지를 포함하지 않습니다. 각 서버에 대 한 hello SQL Server 설치를 실행할 수 있는 위치에 hello 설치 미디어를 배치 합니다.

1. Azure 가상 컴퓨터를 만든 후 RDP와 tooeach 가상 컴퓨터를 연결 합니다.

   RDP와 tooa 가상 컴퓨터를 처음 연결 하면 hello 컴퓨터 묻는 tooallow이 PC toobe hello 네트워크에서 검색할 수 있습니다. **예**를 클릭합니다.

1. Hello SQL Server 기반 가상 컴퓨터 이미지 중 하나를 사용 하는 경우 hello SQL Server 인스턴스를 제거 합니다.

   - **프로그램 및 기능**에서 **Microsoft SQL Server 2016(64비트)**을 마우스 오른쪽 단추로 클릭하고 **제거/변경**을 클릭합니다.
   - **제거**를 클릭합니다.
   - Hello 기본 인스턴스를 선택 합니다.
   - **데이터베이스 엔진 서비스**에서 모든 기능을 제거합니다. **공유 기능**을 제거하지 마십시오. Hello 다음 그림을 참조 하십시오.

      ![기능 제거](./media/virtual-machines-windows-portal-sql-create-failover-cluster/03-remove-features.png)

   - **다음**을 클릭한 후 **제거**를 클릭합니다.

1. <a name="ports"></a>Hello 방화벽 포트를 엽니다.

   각 가상 컴퓨터에서 포트에 나오는 hello Windows 방화벽에 hello를 엽니다.

   | 목적 | TCP 포트 | 참고
   | ------ | ------ | ------
   | SQL Server | 1433 | SQL Server의 기본 인스턴스에 대한 표준 포트입니다. Hello 갤러리에서 이미지를 사용 하는 경우에이 포트는 자동으로 열립니다.
   | 상태 프로브 | 59999 | 모든 공개 TCP 포트입니다. 이후 단계에서 hello 부하 분산 장치 구성 [상태 프로브](#probe) 클러스터 toouse이이 포트 hello 및 합니다.  

1. 저장소 toohello 가상 컴퓨터를 추가 합니다. 자세한 내용은 [저장소 추가](../../../storage/common/storage-premium-storage.md)를 참조하세요.

   두 가상 컴퓨터에 두 개 이상의 데이터 디스크가 필요합니다.

   NTFS 포맷 디스크가 아닌 원시 디스크를 연결합니다.
      >[!NOTE]
      >NTFS 포맷 디스크를 연결하는 경우 디스크 자격 확인 없이 S2D를 사용할 수 있습니다.  

   최소 두 개의 프리미엄 저장소 (SSD 디스크) tooeach VM 연결 합니다. 적어도 P30(1TB) 디스크가 좋습니다.

   집합 호스트 너무 캐싱**읽기 전용**합니다.

   프로덕션 환경에서 사용 하는 hello 스토리지 용량 작업에 따라 달라 집니다. 이 문서에서 설명 하는 hello 값 데모 및 테스트 됩니다.

1. [Hello 가상 컴퓨터 tooyour 기존 도메인을 추가](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain)합니다.

Hello 가상 컴퓨터를 만들고 구성한 후에 hello 장애 조치 클러스터를 구성할 수 있습니다.

## <a name="step-2-configure-hello-windows-failover-cluster-with-s2d"></a>2 단계: S2D와 hello Windows 장애 조치 클러스터 구성

hello 다음 단계와 S2D tooconfigure hello 장애 조치 클러스터입니다. 이 단계에서 수행한 하위 단계 다음 hello:

1. Windows 장애 조치(Failover) 클러스터링 기능 추가
1. Hello 클러스터 유효성 검사
1. Hello 장애 조치 클러스터 만들기
1. Hello 클라우드 미러링 모니터 만들기
1. 저장소 추가

### <a name="add-windows-failover-clustering-feature"></a>Windows 장애 조치(Failover) 클러스터링 기능 추가

1. toobegin, Active Directory의 권한 toocreate 개체 되었으며 로컬 관리자의 멤버인 도메인 계정을 사용 하 여 RDP를 사용 하 여 toohello 첫 번째 가상 컴퓨터를 연결 합니다. Hello 구성의 hello 나머지를 위해이 계정을 사용 합니다.

1. [장애 조치 클러스터링 기능 tooeach 가상 컴퓨터 추가](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms)합니다.

   hello UI에서에서 장애 조치 클러스터링 기능은 tooinstall 두 가상 컴퓨터에서 다음 단계 hello지 않습니다.
   - **서버 관리자**에서 **관리**를 클릭한 다음 **역할 및 기능 추가**를 클릭합니다.
   - **추가 역할 및 기능 마법사**, 클릭 **다음** 너무에 도달할 때까지**기능 선택**합니다.
   - **기능 선택**에서 **장애 조치(Failover) 클러스터링**을 클릭합니다. 모든 필요한 기능 및 hello 관리 도구를 포함 합니다. **기능 추가**를 클릭합니다.
   - 클릭 **다음** 클릭 하 고 **마침** tooinstall hello 기능입니다.

   tooinstall hello 장애 조치 클러스터링 기능은 powershell을 hello 나오는 hello 가상 컴퓨터 중 하나에 따라 관리자 권한 PowerShell 세션에서 스크립트를 실행 합니다.

   ```PowerShell
   $nodes = ("<node1>","<node2>")
   Invoke-Command  $nodes {Install-WindowsFeature Failover-Clustering -IncludeAllSubFeature -IncludeManagementTools}
   ```

Hello 다음 단계를 참조로의 3 단계 hello 지침을 따르십시오 [Windows Server 2016에서 저장소 공간 다이렉트를 사용 하 여 하이퍼 수렴 형 솔루션](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct)합니다.

### <a name="validate-hello-cluster"></a>Hello 클러스터 유효성 검사

이 설명서에서는 아래 tooinstructions [클러스터 유효성 검사](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation)합니다.

Hello UI에서에서 또는 PowerShell을 사용 하는 hello 클러스터의 유효성을 검사 합니다.

UI hello로 toovalidate hello 클러스터 hello 가상 컴퓨터 중 하나에서 다음 단계 hello지 않습니다.

1. **서버 관리자**에서 **도구**를 클릭한 다음 **장애 조치(Failover) 클러스터 관리자**를 클릭합니다.
1. **장애 조치(Failover) 클러스터 관리자**에서 **작업**을 클릭한 다음 **구성 유효성 검사...**를 클릭합니다.
1. **다음**을 누릅니다.
1. **서버 선택 또는 클러스터**, 두 가상 컴퓨터의 형식 hello 이름입니다.
1. **테스트 옵션**에서 **선택한 테스트만 실행**을 선택합니다. **다음**을 누릅니다.
1. **테스트 선택**에서 **저장소**를 제외한 모든 테스트를 포함합니다. Hello 다음 그림을 참조 하십시오.

   ![유효성 검사 테스트](./media/virtual-machines-windows-portal-sql-create-failover-cluster/10-validate-cluster-test.png)

1. **다음**을 누릅니다.
1. **확인**에서 **다음**을 클릭합니다.

hello **유효성 검사 구성 마법사** 실행 hello 유효성 검사 테스트 합니다.

powershell을 실행 hello 가상 컴퓨터 중 하나에 관리자 권한 PowerShell 세션에서 스크립트를 다음과 같은 hello toovalidate hello 클러스터입니다.

   ```PowerShell
   Test-Cluster –Node ("<node1>","<node2>") –Include "Storage Spaces Direct", "Inventory", "Network", "System Configuration"
   ```

Hello 클러스터, 유효성 검사 후 hello 장애 조치 클러스터를 만듭니다.

### <a name="create-hello-failover-cluster"></a>Hello 장애 조치 클러스터 만들기

이 가이드는 너무 참조[hello 장애 조치 클러스터 만들기](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster)합니다.

toocreate hello 장애 조치 클러스터를 해야합니다.
- hello 클러스터 노드 역할을 하는 hello 가상 컴퓨터의 hello 이름입니다.
- Hello 장애 조치 클러스터에 대 한 이름
- Hello 장애 조치 클러스터에 대 한 IP 주소입니다. Hello에 사용 되지 않는 IP 주소를 사용할 수 있습니다 동일한 Azure 가상 네트워크와 서브넷을 클러스터 노드 hello 합니다.

다음 PowerShell hello 장애 조치 클러스터를 만듭니다. Hello hello 노드 (가상 컴퓨터 이름 hello) 이름 사용 하 여 hello 스크립트와 hello Azure VNET에서에서 사용 가능한 IP 주소를 업데이트 합니다.

```PowerShell
New-Cluster -Name <FailoverCluster-Name> -Node ("<node1>","<node2>") –StaticAddress <n.n.n.n> -NoStorage
```   

### <a name="create-a-cloud-witness"></a>클라우드 감시 만들기

클라우드 감시는 Azure Storage Blob에 저장된 새로운 유형의 클러스터 쿼럼 감시입니다. 미러링 모니터 서버 공유를 호스트 하는 별도 VM의 hello 필요성을 제거 합니다.

1. [Hello 장애 조치 클러스터에 대 한 클라우드 감시 만들기](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness)합니다.

1. Blob 컨테이너를 만듭니다.

1. Hello 액세스 키 및 hello 컨테이너 URL을 저장 합니다.

1. Hello 장애 조치 클러스터의 클러스터 쿼럼 감시를 구성 합니다. [Hello 사용자 인터페이스에 구성 hello 쿼럼 감시를] 참조 하십시오. (http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) hello UI에에서 있습니다.

### <a name="add-storage"></a>저장소 추가

hello 디스크 S2D에 대 한 빈 및 파티션 또는 기타 데이터 없이 toobe를 필요합니다. tooclean 디스크에 따라 [이 가이드의 단계를 hello](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks)합니다.

1. [저장소 공간 다이렉트 \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct)를 활성화합니다.

   다음 PowerShell hello 직접 액세스를 저장소 공간을 수 있습니다.  

   ```PowerShell
   Enable-ClusterS2D
   ```

   **장애 조치 클러스터 관리자**, 이제 hello 저장소 풀을 확인할 수 있습니다.

1. [볼륨을 만듭니다](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).

   S2D hello 기능 중 하나는 사용 하도록 설정 하면 저장소 풀을 자동으로 만들 수 있다는 것입니다. 준비 toocreate 볼륨입니다. PowerShell commandlet hello `New-Volume` 서식 toohello 클러스터를 추가 하 고, 클러스터 공유 볼륨 (CSV) 만들기를 포함 하 여 hello 볼륨 만들기 프로세스를 자동화 합니다. hello 다음 예제는 800 기가바이트 (GB) CSV 만듭니다.

   ```PowerShell
   New-Volume -StoragePoolFriendlyName S2D* -FriendlyName VDisk01 -FileSystem CSVFS_REFS -Size 800GB
   ```   

   이 명령이 완료되면 클러스터 리소스로 800GB 볼륨이 탑재됩니다. hello 볼륨이에 `C:\ClusterStorage\Volume1\`합니다.

   다이어그램을 다음 hello S2D 클러스터 공유 볼륨을 보여 줍니다.

   ![ClusterSharedVolume](./media/virtual-machines-windows-portal-sql-create-failover-cluster/15-cluster-shared-volume.png)

## <a name="step-3-test-failover-cluster-failover"></a>3단계: 장애 조치 클러스터의 장애 조치 테스트

장애 조치 클러스터 관리자에서 이동할 수 있는지 hello 저장소 리소스 toohello 다른 클러스터 노드로 확인 합니다. Toohello 장애 조치 클러스터와 연결할 수 있는 경우 **장애 조치 클러스터 관리자** 에서 하나의 노드만 toohello 다른 hello 저장소를 이동 하 고, 준비 tooconfigure hello FCI는 합니다.

## <a name="step-4-create-sql-server-fci"></a>4단계: SQL Server FCI 만들기

Hello 장애 조치 클러스터와 저장소를 포함 하 여 모든 클러스터 구성 요소를 구성 하 고 나면 hello SQL Server FCI를 만들 수 있습니다.

1. RDP와 toohello 첫 번째 가상 컴퓨터를 연결 합니다.

1. **장애 조치 클러스터 관리자**, 모든 클러스터 코어 리소스 hello 첫 번째 가상 컴퓨터에 있는지 확인 합니다. 필요한 경우에 모든 리소스 toothis 가상 컴퓨터를 이동 합니다.

1. Hello 설치 미디어를 찾습니다. Hello 미디어에는 가상 컴퓨터가 hello hello Azure 마켓플레이스 이미지 중 하나를 사용 하는 경우 `C:\SQLServer_<version number>_Full`합니다. **설치**를 클릭합니다.

1. Hello에 **SQL Server 설치 센터**, 클릭 **설치**합니다.

1. **새 SQL Server 장애 조치(failover) 클러스터 설치**를 클릭합니다. Hello 마법사 tooinstall hello SQL Server FCI의에서 hello 지침을 따릅니다.

   hello FCI 데이터 디렉터리 toobe 클러스터 된 저장소에 필요합니다. S2D, 이므로 없이 각 서버에 있는 탑재 지점 tooa 볼륨 하지만 공유 디스크입니다. S2D 두 노드 간에 hello 볼륨을 동기화합니다. hello 볼륨이 클러스터 공유 볼륨으로 toohello 클러스터를 표시 됩니다. Hello 데이터 디렉터리에 대 한 hello CSV 탑재 지점을 사용 합니다.

   ![DataDirectories](./media/virtual-machines-windows-portal-sql-create-failover-cluster/20-data-dicrectories.png)

1. Hello 마법사를 마친 후 설치 프로그램 hello 첫 번째 노드에 SQL Server FCI를 설치 합니다.

1. 성공적으로 설치 hello FCI hello 첫 번째 노드에 설치 된 후 RDP와 toohello 두 번째 노드를 연결 합니다.

1. 열기 hello **SQL Server 설치 센터**합니다. **설치**를 클릭합니다.

1. 클릭 **추가 노드 tooa SQL Server 장애 조치 클러스터**합니다. Hello 마법사 tooinstall SQL server의 hello 지침을 따르고이 서버 toohello FCI를 추가 합니다.

   >[!NOTE]
   >SQL Server와 함께 Azure 마켓플레이스 갤러리 이미지를 사용 하는 경우 SQL Server 도구 hello 이미지와 함께 포함 되었습니다. 이 이미지를 사용 하지 않은 경우 별도로 hello SQL Server 도구를 설치 합니다. [SSMS(SQL Server Management Studio) 다운로드](http://msdn.microsoft.com/library/mt238290.aspx)를 참조하세요.

## <a name="step-5-create-azure-load-balancer"></a>5단계: Azure Load Balancer 만들기

Azure 가상 컴퓨터에서 클러스터는 부하 분산 장치 toohold에 한 번에 하나의 클러스터 노드에서 toobe 필요한 IP 주소를 사용 합니다. 이 솔루션에서는 hello 부하 분산 장치는 SQL Server FCI hello에 대 한 hello IP 주소를 보유합니다.

[Azure Load Balancer를 만들고 구성합니다](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).

### <a name="create-hello-load-balancer-in-hello-azure-portal"></a>Hello Azure 포털에서에서 hello 부하 분산 장치 만들기

toocreate hello 부하 분산 장치:

1. Azure 포털 hello hello 가상 컴퓨터와 toohello 리소스 그룹을 이동 합니다.

1. **+ 추가**를 클릭합니다. 마켓플레이스 검색 hello에 대 한 **부하 분산 장치**합니다. **부하 분산 장치**를 클릭합니다.

1. **만들기**를 클릭합니다.

1. 포함 된 hello 부하 분산 장치를 구성 합니다.

   - **이름**: hello 부하 분산 장치를 식별 하는 이름입니다.
   - **형식**: hello 부하 분산 장치는 모두 public 또는 private 일 수 있습니다. 개인 부하 분산 장치 내에서 액세스할 수 동일한 VNET hello 합니다. 대부분의 Azure 응용 프로그램은 개인 부하 분산 장치를 사용할 수 있습니다. 응용 프로그램에 대 한 액세스 tooSQL 서버 hello 인터넷을 통해 직접 필요한 경우 공용 부하 분산 장치를 사용 합니다.
   - **가상 네트워크**: hello hello 가상 컴퓨터 네트워크에 동일 합니다.
   - **서브넷**: hello 가상 컴퓨터와 동일한 서브넷 hello 합니다.
   - **개인 IP 주소가**: hello toohello SQL Server FCI 클러스터 네트워크 리소스를 할당 하는 동일한 IP 주소입니다.
   - **구독:** 사용자의 Azure 구독입니다.
   - **리소스 그룹**: 사용 하 여 hello 동일한 가상 컴퓨터와 리소스 그룹입니다.
   - **위치**: 사용 하 여 hello 동일한 가상 컴퓨터와 Azure 위치입니다.
   Hello 다음 그림을 참조 하십시오.

   ![CreateLoadBalancer](./media/virtual-machines-windows-portal-sql-create-failover-cluster/30-load-balancer-create.png)

### <a name="configure-hello-load-balancer-backend-pool"></a>Hello 부하 분산 장치 백 엔드 풀을 구성 합니다.

1. Hello 가상 컴퓨터와 toohello Azure 리소스 그룹을 반환 하 고 hello 새 부하 분산 장치를 찾습니다. Toorefresh hello 뷰를 사용할 수 있습니다 있습니다 hello 리소스 그룹에 있습니다. Hello 부하 분산 장치를 클릭 합니다.

1. Hello 부하 분산 장치 블레이드에서 클릭 **백 엔드 풀**합니다.

1. 클릭 **+ 추가** tooadd 백 엔드 풀입니다.

1. Hello 백 엔드 풀에 대 한 이름을 입력 합니다.

1. **가상 컴퓨터 추가**를 클릭합니다.

1. Hello에 **가상 컴퓨터를 선택할** 블레이드에서 클릭 **가용성 집합 선택**합니다.

1. Hello SQL Server 가상 컴퓨터를 배치 하는 hello 가용성 집합을 선택 합니다.

1. Hello에 **가상 컴퓨터를 선택할** 블레이드에서 클릭 **hello 가상 컴퓨터를 선택할**합니다.

   Azure 포털을 가리키도록 다음 그림 hello 같이 표시 됩니다.

   ![CreateLoadBalancerBackEnd](./media/virtual-machines-windows-portal-sql-create-failover-cluster/33-load-balancer-back-end.png)

1. 클릭 **선택** hello에 **가상 컴퓨터를 선택할** 블레이드입니다.

1. **확인** 을 두 번 클릭합니다.

### <a name="configure-a-load-balancer-health-probe"></a>부하 분산 장치 상태 프로브 구성

1. Hello 부하 분산 장치 블레이드에서 클릭 **상태 프로브**합니다.

1. **+ 추가**를 클릭합니다.

1. Hello에 **추가 상태 프로브** 블레이드에서 <a name="probe"> </a>hello 상태 프로브 매개 변수를 설정 합니다.

   - **이름**: hello 상태 검색에 대 한 이름입니다.
   - **프로토콜**: TCP입니다.
   - **포트**: tooan 사용 가능한 TCP 포트를 설정 합니다. 이 포트에는 공개 방화벽 포트가 필요합니다. 사용 하 여 hello [동일한 포트](#ports) hello 방화벽에서 hello 상태 검색에 대 한 설정입니다.
   - **간격**: 5초입니다.
   - **비정상 임계값**: 두 번 연속 실패입니다.

1. 확인을 클릭합니다.

### <a name="set-load-balancing-rules"></a>부하 분산 규칙 설정

1. Hello 부하 분산 장치 블레이드에서 클릭 **부하 분산 규칙**합니다.

1. **+ 추가**를 클릭합니다.

1. Hello 부하 분산 규칙 매개 변수 설정:

   - **이름**: hello 부하 분산 규칙에 대 한 이름입니다.
   - **프런트 엔드 IP 주소**: hello SQL Server FCI의 클러스터 네트워크 리소스에 대 한 hello IP 주소를 사용 합니다.
   - **포트**: hello SQL Server FCI TCP 포트에 대해 설정 합니다. hello 기본 인스턴스가 포트는 1433입니다.
   - **백 엔드 포트가**:이 값이 동일한 포트 hello를 사용 하 여 hello로 **포트** 사용 하도록 설정 하면 값 **부동 IP (직접 서버 반환)**합니다.
   - **백 엔드 풀**: 이전에 구성 된 사용 하 여 hello 백 엔드 풀 이름입니다.
   - **상태 프로브**: 이전에 구성 된 사용 하 여 hello 상태 검색 합니다.
   - **세션 지속성**: 없음.
   - **유휴 제한 시간(분)**: 4.
   - **부동 IP(Direct Server Return)**: 사용

1. **확인**을 클릭합니다.

## <a name="step-6-configure-cluster-for-probe"></a>6단계: 프로브에 대한 클러스터 구성

PowerShell에서 hello 클러스터 프로브 포트 매개 변수를 설정 합니다.

tooset hello 클러스터 프로브 포트 매개 변수, 사용자 환경에서 스크립트를 다음 hello에서 변수를 업데이트 합니다.

  ```PowerShell
   $ClusterNetworkName = "<Cluster Network Name>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name).
   $IPResourceName = "IP Address Resource Name" # hello IP Address cluster resource name.
   $ILBIP = "<10.0.0.x>" # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
   [int]$ProbePort = <59999>

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```


## <a name="step-7-test-fci-failover"></a>7단계: FCI 장애 조치(failover) 테스트

장애 조치의 hello FCI toovalidate 클러스터 기능을 테스트 합니다. 다음 단계 hello 마십시오.

1. RDP tooone hello SQL Server FCI의 클러스터 노드를 연결 합니다.

1. **장애 조치(Failover) 클러스터 관리자**를 엽니다. **역할**을 클릭합니다. Hello SQL Server FCI 역할을 소유 하는 노드를 확인 합니다.

1. Hello SQL Server FCI 역할을 마우스 오른쪽 단추로 클릭 합니다.

1. **이동**을 클릭하고 **가장 적합한 노드**를 클릭합니다.

**장애 조치 클러스터 관리자** 표시 hello 역할 및 리소스를 오프 라인 상태가 됩니다. hello 리소스 이동 하 고 온라인 상태로 전환에 다른 노드를 hello 합니다.

### <a name="test-connectivity"></a>연결 테스트

tootest 연결, 로그 hello에 tooanother 가상 컴퓨터에 동일한 가상 네트워크입니다. 열기 **SQL Server Management Studio** toohello SQL Server FCI 이름을 연결 합니다.

>[!NOTE]
>필요한 경우 [SQL Server Management Studio를 다운로드](http://msdn.microsoft.com/library/mt238290.aspx)할 수 있습니다.

## <a name="limitations"></a>제한 사항
Azure 가상 컴퓨터에 Microsoft Distributed Transaction Coordinator (DTC)는 hello RPC 포트 hello 부하 분산 장치에서 지원 되지 않으므로 Fci에서 지원 되지 않습니다.

## <a name="see-also"></a>참고 항목

[원격 데스크톱(Azure)을 사용하여 S2D 설치](http://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-storage-spaces-direct-deployment)

[저장소 공간 다이렉트를 사용하는 하이퍼 수렴형 솔루션](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct)

[저장소 공간 다이렉트 개요](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)

[S2D에 대한 SQL Server 지원](https://blogs.technet.microsoft.com/dataplatforminsider/2016/09/27/sql-server-2016-now-supports-windows-server-2016-storage-spaces-direct/)
