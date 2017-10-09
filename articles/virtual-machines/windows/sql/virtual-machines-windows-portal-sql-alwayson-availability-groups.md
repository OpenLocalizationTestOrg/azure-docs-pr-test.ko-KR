---
title: "Azure 리소스 관리자 Vm에 대 한 고가용성을 aaaSet | Microsoft Docs"
description: "이 자습서에서는 toocreate Always On 가용성 Azure 리소스 관리자 모드에서 Azure 가상 컴퓨터를 그룹화 하는 방법을 보여 줍니다."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 64e85527-d5c8-40d9-bbe2-13045d25fc68
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: 6f0a253d3502259a487e66fd62d92e41c379a6b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-always-on-availability-groups-in-azure-virtual-machines-automatically-resource-manager"></a>Azure Virtual Machines에서 자동으로 Always On 가용성 그룹 구성: Resource Manager

이 자습서에서는 toocreate SQL Server 가용성 사용 하 여 Azure 리소스 관리자 가상 컴퓨터를 그룹화 하는 방법을 보여 줍니다. hello 자습서에서는 Azure 블레이드 tooconfigure 서식 파일을 사용 합니다. Hello 기본 설정을 검토 하 고, 필요한 설정을 입력 하 고,이 자습서를 살펴보면서 hello 블레이드 hello 포털에서를 업데이트할 수 있습니다.

hello 전체 자습서는 Azure 가상 컴퓨터에서 hello 다음 요소를 포함 하는 SQL Server 가용성 그룹을 만듭니다.

* 프런트 엔드 및 백 엔드 서브넷을 비롯한 여러 서브넷을 포함하는 가상 네트워크
* Active Directory 도메인을 포함하는 두 개의 도메인 컨트롤러
* SQL Server를 실행 하는 배포 된 toohello 백 엔드 서브넷 및 Active Directory 도메인에 가입된 toohello 두 가상 컴퓨터
* Hello 노드 과반수 쿼럼 모델을 사용 하 여 3 개 노드 장애 조치 클러스터
* 가용성 데이터베이스의 두 개의 동기 커밋 복제본이 포함된 가용성 그룹

다음 그림 hello hello 완벽 한 솔루션을 나타냅니다.

![Azure에서 가용성 그룹에 대한 테스트 랩 아키텍처](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/0-EndstateSample.png)

이 솔루션의 모든 리소스에 포함할 tooa 단일 리소스 그룹입니다.

이 자습서를 시작 하기 전에 hello 다음을 확인 합니다.

* Azure 계정이 있습니다. 계정이 없는 경우 [평가판 계정에 등록](http://azure.microsoft.com/pricing/free-trial/)합니다.
* 이미 어떻게 toouse hello GUI tooprovision hello 가상 컴퓨터 갤러리에서 SQL Server 가상 컴퓨터를 알고 있습니다. 자세한 내용은 [Azure에서 SQL Server 가상 컴퓨터 프로비전](virtual-machines-windows-portal-sql-server-provision.md)을 참조하세요.
* 가용성 그룹을 확실하게 이해하고 있습니다. 자세한 내용은 [Always On 가용성 그룹(SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx)을 참조하세요.

> [!NOTE]
> SharePoint와 가용성 그룹을 사용하는 것에 관심이 있는 경우 [SharePoint 2013에 대해 SQL Server 2012 Always On 가용성 그룹 구성](http://technet.microsoft.com/library/jj715261.aspx)을 참조하세요.
>
>

이 자습서에서는 Azure hello를 포털:

* Hello 포털에서 템플릿을 Always On hello를 선택 합니다.
* Hello 템플릿 설정을 검토 하 고 사용자 환경에 대 한 몇 가지 구성 설정을 업데이트 합니다.
* Hello 전체 환경을 만들 때 Azure를 모니터링 합니다.
* Tooa 도메인 컨트롤러와 SQL Server를 실행 하는 tooa 서버 연결 합니다.

[!INCLUDE [availability-group-template](../../../../includes/virtual-machines-windows-portal-sql-alwayson-ag-template.md)]

## <a name="provision-hello-cluster-from-hello-gallery"></a>Hello 갤러리에서 프로 비전 hello 클러스터
Azure는 hello 전체 솔루션에 대 한 갤러리 이미지를 제공합니다. toolocate hello 템플릿:

1. 사용자 계정을 사용 하 여 Azure 포털 toohello에 로그인 합니다.
2. Hello Azure 포털에서에서 클릭 **+ 새로 만들기** tooopen hello **새로** 블레이드입니다.
3. Hello에 **새로** 블레이드에 대 한 검색 **AlwaysOn**합니다.
   ![AlwaysOn 템플릿 찾기](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/16-findalwayson.png)
4. Hello 검색 결과 **SQL Server AlwaysOn 클러스터**합니다.
   ![AlwaysOn 템플릿](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/17-alwaysontemplate.png)
5. **배포 모델 선택**에서 **Resource Manager**를 선택합니다.

### <a name="basics"></a>기본 사항
클릭 **기본 사항** 및 hello 다음 설정을 구성 합니다.

* **관리자 사용자 이름** 도메인 관리자 권한이 있는 사용자 계정을 이며 SQL Server의 두 인스턴스가 hello SQL Server sysadmin 고정된 서버 역할의 멤버입니다. 이 자습서에서는 **DomainAdmin**을 사용합니다.
* **암호** hello 도메인 관리자 계정에 대 한 hello 암호입니다. 복잡한 암호를 사용합니다. Hello 암호를 확인 합니다.
* **구독** Azure hello 가용성 그룹에 대 한 모든 배포 toorun 리소스를 청구 하는 hello 구독입니다. 계정에 여러 구독이 있는 경우 다른 구독을 지정할 수 있습니다.
* **리소스 그룹** hello 그룹 toowhich 속해이 서식 파일에 의해 만들어진 모든 Azure 리소스에 대 한 hello 이름입니다. 이 자습서에서는 **SQL-HA-RG**를 사용합니다. 자세한 내용은 [Azure Resource Manager 개요](../../../azure-resource-manager/resource-group-overview.md#resource-groups)를 참조하세요.
* **위치** hello 자습서 hello 리소스를 만들어 위치는 Azure 지역 hello 됩니다. Azure 지역을 선택합니다.

hello 다음 스크린 샷에서 완료 된 **기본 사항** 블레이드:

![기본 사항](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/1-basics.png)

**확인**을 클릭합니다.

### <a name="domain-and-network-settings"></a>도메인 및 네트워크 설정
이 Azure 갤러리 템플릿은 도메인 및 도메인 컨트롤러를 만듭니다. 또한 네트워크와 두 개의 서브넷을 만듭니다. hello 서식 파일은 기존 도메인 또는 가상 네트워크에 서버를 만들 수 없습니다. hello 다음 단계는 hello 도메인 및 네트워크 설정을 구성합니다.

Hello에 **도메인 및 네트워크 설정** 블레이드를 검토 hello 미리 hello 도메인 및 네트워크 설정에 대 한 값을 설정 합니다.

* **포리스트 루트 도메인 이름** hello 도메인 이름이 hello Active Directory 도메인에 대 한 해당 호스트 hello 클러스터입니다. Hello 자습서에서 사용 하 여 **contoso.com**합니다.
* **가상 네트워크 이름** hello Azure 가상 네트워크에 대 한 hello 네트워크 이름입니다. Hello 자습서에서 사용 하 여 **autohaVNET**합니다.
* **도메인 컨트롤러 서브넷 이름** hello 가상 네트워크의 한 부분 hello 이름 해당 호스트 hello 도메인 컨트롤러입니다. **subnet-1**을 사용합니다. 이 서브넷은 주소 접두사 **10.0.0.0/24**를 사용합니다.
* **SQL Server 서브넷 이름** hello 일부 SQL Server 및 hello 파일을 실행 하는 호스트 hello 서버 공유 감시 hello 가상 네트워크의 이름입니다. **subnet-2**를 사용합니다. 이 서브넷은 주소 접두사 **10.0.1.0/26**을 사용합니다.

Azure에서 가상 네트워크에 대해 자세히 toolearn 참조 [가상 네트워크 개요](../../../virtual-network/virtual-networks-overview.md)합니다.  

hello **도메인 및 네트워크 설정** 해야 hello와 비슷한 모양의 다음 스크린 샷:

![도메인 및 네트워크 설정](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/2-domain.png)

필요한 경우에 이러한 값을 변경할 수 있습니다. 이 자습서에서 사용 하 여 hello 사전 값을 설정 합니다.

Hello 설정을 검토 한 다음 클릭 **확인**합니다.

### <a name="availability-group-settings"></a>가용성 그룹 설정
**가용성 그룹 설정**, 검토 hello hello 가용성 그룹에 대 한 값을 사전 설정 및 수신기 hello 합니다.

* **가용성 그룹 이름** hello 가용성 그룹에 대 한 hello 클러스터 된 리소스 이름입니다. 이 자습서에서는 **Contoso-ag**를 사용합니다.
* **가용성 그룹 수신기 이름을** hello 클러스터 및 hello 내부 부하 분산 장치에서 사용 됩니다. TooSQL 서버를 연결 하는 클라이언트는이 이름 tooconnect toohello 적절 한 데이터베이스의 복제본 hello 사용할 수 있습니다. 이 자습서에서는 **Contoso-listener**를 사용합니다.
* **가용성 그룹 수신기 포트** hello SQL Server 수신기의 hello TCP 포트를 지정 합니다. 이 자습서에 대 한 hello 기본 포트를 사용 하 여 **1433**합니다.

필요한 경우에 이러한 값을 변경할 수 있습니다. 이 자습서에서 사용 하 여 hello 사전 값을 설정 합니다.  

![가용성 그룹 설정](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/3-availabilitygroup.png)

**확인**을 클릭합니다.

### <a name="virtual-machine-size-storage-settings"></a>가상 컴퓨터 크기, 저장소 설정
**VM 크기, 저장소 설정**, SQL Server 가상 컴퓨터 크기를 선택 하 고 검토 hello 다른 설정 합니다.

* **SQL Server 가상 컴퓨터 크기** SQL Server를 실행 하는 두 가상 컴퓨터에 대 한 hello 크기입니다. 워크로드에 적합한 가상 컴퓨터 크기를 선택합니다. 이 환경을 hello 자습서 빌드하는 경우 사용 하 여 **DS2**합니다. 프로덕션 작업에 대 한 hello 작업 부하를 지원할 수 있는 가상 컴퓨터 크기를 선택 합니다. 대부분의 프로덕션 워크로드에서는 **DS4** 이상이 필요합니다. hello 템플릿이이 크기의 두 가상 컴퓨터를 빌드하고 각 SQL Server를 설치 합니다. 자세한 내용은 [가상 컴퓨터의 크기](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.

> [!NOTE]
> Azure 설치 hello SQL Server의 Enterprise Edition입니다. hello 비용 hello 버전과 hello 가상 컴퓨터 크기에 따라 달라 집니다. 현재 비용에 대한 자세한 내용은 [가상 컴퓨터 가격 책정](http://azure.microsoft.com/pricing/details/virtual-machines/#Sql)을 참조하세요.
>
>

* **도메인 컨트롤러 가상 컴퓨터 크기** hello hello 가상 컴퓨터 크기는 도메인 컨트롤러입니다. 이 자습서에서는 **D2**를 사용합니다.
* **파일 공유 감시 가상 컴퓨터 크기** hello 파일 공유 감시에 대 한 hello 가상 컴퓨터 크기입니다. 이 자습서에서는 **A1**을 사용합니다.
* **SQL 저장소 계정** hello hello SQL Server 데이터 및 운영 체제 디스크를 보유 하는 hello 저장소 계정의 이름입니다. 이 자습서에서는 **alwaysonsql01**을 사용합니다.
* **DC 저장소 계정** 는 hello hello 저장소 계정의 이름으로 hello에 대 한 도메인 컨트롤러입니다. 이 자습서에서는 **alwaysondc01**을 사용합니다.
* **SQL Server 데이터 디스크 크기** TB에서 t B의 hello SQL Server 데이터 디스크의 hello 크기입니다. 1~4 사이에서 숫자를 지정합니다. 이 자습서에서는 **1**을 사용합니다.
* **저장소 최적화** hello 작업 형식에 따라 hello SQL Server 가상 컴퓨터에 대 한 특정 저장소 구성 설정을 설정 합니다. 이 시나리오에서는 모든 SQL Server 가상 컴퓨터 tooread 전용으로 설정 된 Azure 디스크 호스트 캐시와 프리미엄 저장소를 사용 합니다. 또한 이러한 세 가지 설정 중 하나를 선택 하 여 hello 작업에 대 한 SQL Server 설정을 최적화할 수 있습니다.

  * **일반 워크로드**는 특정 구성 설정을 설정하지 않음
  * **트랜잭션 처리**는 추적 플래그 1117 및 1118을 설정함
  * **데이터 웨어하우징**은 추적 플래그 1117 및 610을 설정함

이 자습서에서는 **일반 워크로드**를 사용합니다.

![VM 크기 저장소 설정](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/4-vm.png)

Hello 설정을 검토 한 다음 클릭 **확인**합니다.

#### <a name="a-note-about-storage"></a>저장소에 대한 정보
추가 최적화 hello SQL Server 데이터 디스크의 hello 크기에 따라 달라 집니다. 데이터 디스크의 각 테라바이트에 대해 Azure는 1TB Premium Storage를 더 추가합니다. 서버 네 대까지 또는 그 이상의 필요한 hello 템플릿 각 SQL Server 가상 컴퓨터에 저장소 풀을 만듭니다. 저장소 풀은 여러 디스크는 구성 된 tooprovide 더 높은 용량, 복원 력 및 성능 일종의 저장소 가상화 합니다.  그런 다음 hello 서식 파일 저장소 공간 hello 저장소 풀에 만들고 단일 데이터 디스크 toohello 운영 체제를 표시 합니다. hello 템플릿 SQL Server에 대 한 hello 데이터 디스크로이 디스크를 지정합니다. SQL Server에 대 한 hello 저장소 풀 설정에 따라 hello를 사용 하 여 튜닝 하는 hello 템플릿:

* 스트라이프 크기는 hello interleave hello 가상 디스크에 대 한 설정입니다. 트랜잭션 워크로드에는 64KB가 사용되고, 데이터 웨어하우징 워크로드에는 256KB가 사용됩니다.
* 복원력은 단순합니다(복원력 없음).

> [!NOTE]
> Azure 프리미엄 저장소는 로컬로 중복 하 고 hello 데이터 복사본이 3 개 단일 지역 내 hello 저장소 풀에 추가 복원 력이 필요 하지 않도록 합니다.
>
>

* 열 수가 hello 저장소 풀의 디스크 hello 수와 일치 합니다.

저장소 공간 및 저장소 풀에 대한 자세한 내용은 다음을 참조하세요.

* [저장소 공간 개요](http://technet.microsoft.com/library/hh831739.aspx)
* [Windows Server 백업 및 저장소 풀](http://technet.microsoft.com/library/dn390929.aspx)

SQL Server 구성 모범 사례에 대한 자세한 내용은 [Azure 가상 컴퓨터의 SQL Server에 대한 성능 모범 사례](virtual-machines-windows-sql-performance.md)를 참조하세요.

### <a name="sql-server-settings"></a>SQL 서버 설정
**SQL Server 설정을**, 검토 및 hello SQL Server 가상 컴퓨터 이름 접두사, SQL Server 버전, SQL Server 서비스 계정 및 암호를 수정 하 고 SQL 자동 패치 유지 관리 일정 hello 합니다.

* **SQL Server 이름 접두사** 이름인 toocreate 사용 되는 각 SQL Server 가상 컴퓨터에 대 한 합니다. 이 자습서에서는 **sqlserver**를 사용합니다. hello 템플릿 이름을 hello SQL Server 가상 컴퓨터 *sqlserver-0* 및 *sqlserver-1*합니다.
* **SQL Server 버전** SQL Server의 hello 버전입니다. 이 자습서에서는 **SQL Server 2014**를 사용합니다. 또한 **SQL Server 2012** 또는 **SQL Server 2016**을 선택할 수 있습니다.
* **SQL Server 서비스 계정 사용자 이름** hello SQL Server 서비스에 대 한 hello 도메인 계정 이름입니다. 이 자습서에서는 **sqlservice**를 사용합니다.
* **암호** hello SQL Server 서비스 계정에 대 한 hello 암호입니다.  복잡한 암호를 사용합니다. Hello 암호를 확인 합니다.
* **유지 관리 일정 SQL 자동 패치** hello 요일 hello Azure에 자동으로 hello SQL Server 패치를 식별 합니다. 이 자습서에서는 **일요일**을 입력합니다.
* **SQL 자동 패치 유지 관리 시작 시간** 자동 패치 적용을 시작할 때 hello Azure 지역에 대 한 hello 시간 됩니다.

> [!NOTE]
> 각 가상 컴퓨터에 대 한 창 패치 hello 한 시간 지연 됩니다. 가상 컴퓨터가 하나만 시간 tooprevent 중단 서비스에서 패치 됩니다.
>
>

![SQL 서버 설정](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/5-sql.png)

Hello 설정을 검토 한 다음 클릭 **확인**합니다.

### <a name="summary"></a>요약
Hello 요약 페이지에서 Azure hello 설정을 확인 합니다. 또한 hello 서식 파일을 다운로드할 수 있습니다. 검토 hello를 요약 합니다. **확인**을 클릭합니다.

### <a name="buy"></a>구입
이 마지막 블레이드에는 **사용 약관** 및 **개인정보취급방침**이 포함됩니다. 이 정보를 검토합니다. Azure toostart toocreate hello 가상 컴퓨터에 대 한 준비가 하 고 모든 hello hello 가용성 그룹에 대 한 다른 필수 리소스를 클릭 하 여 **만들기**합니다.

Azure 포털 hello hello 리소스 그룹 및 모든 hello 리소스를 만듭니다.

## <a name="monitor-deployment"></a>배포 모니터링
Hello Azure 포털에서에서 hello 배포 진행률을 모니터링 합니다. Hello 배포를 표시 하는 아이콘은 자동으로 고정 된 toohello Azure 포털 대시보드에서입니다.

![Azure 대시보드](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/11-deploydashboard.png)

## <a name="connect-toosql-server"></a>TooSQL 서버 연결
SQL Server의 새 인스턴스를 hello 인터넷에 연결 된 IP 주소를 가진 가상 컴퓨터에서 실행 됩니다. 원격 데스크톱 (RDP) 직접 tooeach SQL Server 가상 컴퓨터를 수 있습니다.

tooRDP tooa SQL Server는 다음이 단계를 따르십시오.

1. Azure 포털 대시보드에서 hello에서 hello 배포 성공 했다는 것을 확인 합니다.
2. **리소스**를 클릭합니다.
3. Hello에 **리소스** 블레이드에서 클릭 **sqlserver-0**,이 SQL Server를 실행 하는 hello 가상 컴퓨터 중 하나의 hello 컴퓨터 이름입니다.
4. 에 대 한 hello 블레이드에서 **sqlserver-0**, 클릭 **연결**합니다. 브라우저는 tooopen 원하는 또는 hello 원격 연결 개체를 저장할 경우 요청 합니다. **열기**를 클릭합니다.
5. **원격 데스크톱 연결** 수 있어도 경고는 hello이 원격 연결의 게시자를 식별할 수 없습니다. **Connect**를 클릭합니다.
6. Windows 보안 메시지 있습니다 tooenter hello 주 도메인 컨트롤러의 사용자 자격 증명 tooconnect toohello IP 주소를 표시합니다. **다른 계정 사용**을 클릭합니다. **사용자 이름**에 **contoso\DomainAdmin**을 입력합니다. Hello 서식 파일에 hello 관리자 사용자 이름을 설정 하는 경우이 계정을 구성 했습니다. Hello 템플릿을 구성할 때 선택한 hello 복잡 한 암호를 사용 합니다.
7. **원격 데스크톱** hello 원격 컴퓨터를 인증할 수 없는 due을 경고 하의 보안 인증서에 tooproblems 합니다. 표시 hello 보안 인증서 이름입니다. Hello 이름이 hello 자습서를 따른 경우 **sqlserver 0.contoso.com**합니다. **예**를 클릭합니다.

RDP toohello SQL Server 가상 컴퓨터와 연결 되어 있습니다. SQL Server Management Studio를 열고 지정, SQL Server의 기본 인스턴스 toohello 연결 및 해당 hello 가용성 그룹 구성 되어 있는지 확인 합니다.
