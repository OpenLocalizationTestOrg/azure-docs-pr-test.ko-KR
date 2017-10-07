---
title: "서버 가용성 그룹-Azure 가상 컴퓨터-자습서 aaaSQL | Microsoft Docs"
description: "이 자습서에서는 어떻게 toocreate는 SQL Server Always On 가용성 그룹에 Azure 가상 컴퓨터."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 08a00342-fee2-4afe-8824-0db1ed4b8fca
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/09/2017
ms.author: mikeray
ms.openlocfilehash: 65b4210b0f851828a32a02053b03e4b8d469ba4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-always-on-availability-group-in-azure-vm-manually"></a>수동으로 Azure VM에서 Always On 가용성 그룹 구성

이 자습서에서는 어떻게 toocreate는 SQL Server Always On 가용성 그룹에 Azure 가상 컴퓨터. hello 전체 자습서는 두 명의 SQL Server에서 데이터베이스 복제본으로 가용성 그룹을 만듭니다.

**예상 시간**: hello 전제 조건이 충족 되 면 약 30 분 toocomplete를 사용 합니다.

hello 다이어그램 hello 자습서에서 빌드할 보여 줍니다.

![가용성 그룹](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

## <a name="prerequisites"></a>필수 조건

hello 자습서에서는 SQL Server Always On 가용성 그룹에 대 한 기본적인 이해 있다고 가정 합니다. 자세한 내용은 [Always On 가용성 그룹 개요(SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx)를 참조하세요.

hello 다음 표에이 자습서를 시작 하기 전에 toocomplete 해야 하는 hello 필수 구성 요소.

|  |요구 사항 |설명 |
|----- |----- |----- |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png) | SQL Server 2개 | - Azure 가용성 집합에 <br/> - 단일 도메인에 <br/> - 장애 조치(Failover) 클러스터링 기능(설치됨) |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)| Windows Server | 클러스터 감시를 위한 파일 공유 |  
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|SQL Server 서비스 계정 | 도메인 계정 |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|SQL Server 에이전트 서비스 계정 | 도메인 계정 |  
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|방화벽 포트 열기 | - SQL Server: 기본 인스턴스에 대해 **1433** <br/> - 데이터베이스 미러링 끝점: **5022** 또는 사용 가능한 포트 <br/> - Azure Load Balancer 프로브: **59999** 또는 사용 가능한 포트 |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|장애 조치(Failover) 클러스터링 기능 추가 | 이 기능을 필요로 하는 SQL Server 2개 |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|설치 도메인 계정 | - 각 SQL Server의 로컬 관리자 <br/> - SQL Server의 각 인스턴스에 대해 SQL Server sysadmin 고정 서버 역할의 멤버  |


너무 필요한 hello 자습서를 시작 하기 전에[Azure 가상 컴퓨터의 Always On 가용성 그룹을 만들기 위한 사전 요구 사항을 완료](virtual-machines-windows-portal-sql-availability-group-prereq.md)합니다. 이러한 필수 구성이 요소는 이미 완료 되 면 이동할 수 있습니다 너무[클러스터 만들기](#CreateCluster)합니다.


<!--**Procedure**: *This is hello first “step”. Make titles H2’s and short and clear – H2’s appear in hello right pane on hello web page and are important for navigation.*-->

<a name="CreateCluster"></a>
##Hello 클러스터 만들기

필수 구성 요소를 완료 하는 hello, 후 hello 첫 번째 단계는 toocreate 두 SQL Sever 포함 된 Windows Server 장애 조치 클러스터와 미러링 모니터 서버입니다.  

1. RDP toohello SQL 서버와 미러링 모니터 서버 hello에 관리자가 있는 도메인 계정을 사용 하 여 첫 번째 SQL Server.

   >[!TIP]
   >Hello를 따른 경우 [필수 사항 문서](virtual-machines-windows-portal-sql-availability-group-prereq.md)를 호출 하는 계정을 만든 **CORP\Install**합니다. 이 계정을 사용합니다.

2. Hello에 **서버 관리자** 대시보드에서 **도구**, 클릭 하 고 **장애 조치 클러스터 관리자**합니다.
3. Hello 왼쪽된 창에서 마우스 오른쪽 단추로 클릭 **장애 조치 클러스터 관리자**, 클릭 하 고 **클러스터 만들기**합니다.
   ![클러스터 만들기](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)
4. 클러스터 만들기 마법사 hello 하 다음 표에 hello에 hello 설정을 사용 하 여 hello 페이지를 단계별로 실행 하 여 1 노드 클러스터 만들기:

   | Page | 설정 |
   | --- | --- |
   | 시작하기 전에 |기본값 사용 |
   | 서버 선택 |첫 번째 SQL Server의 이름을 지정 하는 형식 hello **서버 이름을 입력** 클릭 **추가**합니다. |
   | 유효성 검사 경고 |선택 **아니요.가이 클러스터에 대 한 Microsoft의 지원이 필요 하지 않으며 따라서 toorun hello 유효성 검사를 원하지 않는 I를 테스트 합니다. 다음을 클릭 하면 hello 클러스터 만들기를 계속**합니다. |
   | 클러스터 관리 hello에 대 한 액세스 지점 |클러스터 이름(예: **SQLAGCluster1**)을 **클러스터 이름**에 입력합니다.|
   | 다음 |저장소 공간을 사용하지 않는 경우 기본값을 사용합니다. 이 표 아래 hello 참고를 참조 하십시오. |

### <a name="set-hello-cluster-ip-address"></a>Hello 클러스터 IP 주소 설정

1. **장애 조치 클러스터 관리자**, 너무 아래로 스크롤하여**클러스터 코어 리소스** hello 클러스터 세부 정보를 확장 합니다. 두 hello 표시 되어야 **이름** 및 hello **IP 주소** hello의 리소스 **실패** 상태입니다. hello IP 주소 리소스 상태로 만들 수 없습니다 온라인 hello 클러스터 hello 지정 되기 때문에 자체 hello 컴퓨터와 동일한 IP 주소를 사용 하므로 중복 된 주소입니다.

2. 마우스 오른쪽 단추로 클릭 hello 실패 **IP 주소** 리소스 및 클릭 **속성**합니다.

   ![클러스터 속성](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/42_IPProperties.png)

3. 선택 **고정 IP 주소** 하 고 SQL Server hello hello 주소 텍스트 상자에는 서브넷에서 사용 가능한 주소를 지정 합니다. 그런 다음 **확인**을 클릭합니다.
4. Hello에 **클러스터 코어 리소스** 섹션 클러스터 이름을 마우스 오른쪽 단추로 클릭 하 고 클릭 **온라인 상태로 만들기**합니다. 그런 다음 두 리소스가 모두 온라인 상태로 전환될 때까지 기다립니다. Hello 클러스터 이름 리소스가 온라인 상태가 되 면 새 AD 컴퓨터 계정으로 hello DC 서버를 업데이트 합니다. 이 AD 계정 toorun hello 나중에 가용성 그룹 클러스터형 서비스를 사용 합니다.

### <a name="addNode"></a>추가 다른 SQL Server toocluster hello

추가 다른 SQL Server toohello 클러스터 hello 합니다.

1. Hello 브라우저 트리에서 hello 클러스터를 마우스 오른쪽 단추로 클릭 하 고 클릭 **노드 추가**합니다.

    ![노드 toohello 클러스터를 추가 합니다.](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/44-addnode.png)

1. Hello에 **노드 추가 마법사**, 클릭 **다음**합니다. Hello에 **서버 선택** 페이지에서 추가할 두 번째 SQL Server hello 합니다. 형식 hello 서버 이름은 **서버 이름을 입력** 클릭 하 고 **추가**합니다. 완료하면 **다음**을 클릭합니다.

1. Hello에 **유효성 검사 경고** 페이지 **아니요** (프로덕션 시나리오에 테스트를 수행 해야 hello 유효성 검사). 그런 후 **다음**을 클릭합니다.

8. Hello에 **확인** 페이지에서 저장소 공간을 일반 hello 확인란을 사용 하는 경우 **모든 적합 한 저장소 toohello 클러스터를 추가 합니다.**

   ![노드 확인 추가](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/46-addnodeconfirmation.png)

    >[!WARNING]
   >저장소 공간을 사용 하는 경우 및 선택을 취소 하지 않으면 **모든 적합 한 저장소 toohello 클러스터 추가**, Windows hello 프로세스를 클러스터링 하는 동안 hello 가상 디스크를 분리 합니다. 결과적으로, 이러한 hello 저장소 공간을 hello 클러스터에서 제거 될 때까지 디스크 관리자 또는 탐색기에 표시 되지 않습니다 및 PowerShell을 사용 하 여 다시 연결 합니다. 저장소 공간 toostorage 풀의 여러 디스크를 그룹화 합니다. 자세한 내용은 [저장소 공간](https://technet.microsoft.com/library/hh831739)을 참조하세요.

1. **다음**을 클릭합니다.

1. **마침**을 클릭합니다.

   장애 조치 클러스터 관리자에서는 클러스터에 새 노드가 고 hello에 나열 **노드** 컨테이너입니다.

10. 로그 아웃 hello 원격 데스크톱 세션.

### <a name="add-a-cluster-quorum-file-share"></a>클러스터 쿼럼 파일 공유 추가

이 예제에서는 hello Windows 클러스터 파일 공유 toocreate 클러스터 쿼럼을 사용합니다. 이 자습서에서는 노드 및 파일 공유 과반수 쿼럼을 사용합니다. 자세한 내용은 [장애 조치(Failover) 클러스터의 쿼럼 구성 이해](http://technet.microsoft.com/library/cc731739.aspx)를 참조하세요.

1. 원격 데스크톱 세션 toohello 파일 공유 미러링 모니터 멤버 서버를 연결 합니다.

1. **서버 관리자**에서 **도구**를 클릭합니다. **컴퓨터 관리**를 엽니다.

1. **공유 폴더**를 클릭합니다.

1. **공유**를 마우스 오른쪽 단추로 클릭하고 **새 공유...**를 클릭합니다.

   ![새 공유](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   사용 하 여 **공유 폴더 만들기 마법사** toocreate를 공유 합니다.

1. **폴더 경로**, 클릭 **찾아보기** 를 찾거나 hello 공유 폴더에 대 한 경로 만듭니다. **다음**을 누릅니다.

1. **이름, 설명 및 설정을** hello 공유 이름 및 경로 확인 합니다. **다음**을 누릅니다.

1. **공유 폴더 사용 권한**에서 **사용 권한 사용자 지정**을 설정합니다. **사용자 지정...**을 클릭합니다.

1. **사용 권한 사용자 지정**에서 **추가...**를 클릭합니다.

1. 해당 hello 사용 되는 계정 toocreate hello 클러스터에 모든 권한이 있는지 확인 합니다.

   ![새 공유](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/50-filesharepermissions.png)

1. **확인**을 클릭합니다.

1. **공유 폴더 사용 권한**에서 **마침**을 클릭합니다. **마침**을 다시 클릭합니다.  

1. 로그 아웃 hello 서버

### <a name="configure-cluster-quorum"></a>클러스터 쿼럼 구성

다음으로 hello 클러스터 쿼럼을 설정 합니다.

1. 원격 데스크톱 toohello 첫 번째 클러스터 노드를 연결 합니다.

1. **장애 조치 클러스터 관리자**hello 클러스터를 마우스 오른쪽 단추로 너무 가리킨**기타 작업**를 클릭 하 고 **클러스터 쿼럼 설정 구성 중... **.

   ![새 공유](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/52-configurequorum.png)

1. **클러스터 쿼럼 구성 마법사**에서 **다음**을 클릭합니다.

1. **쿼럼 구성 옵션 선택**, 선택 **hello 쿼럼 감시 선택**를 클릭 하 고 **다음**합니다.

1. **쿼럼 감시 선택**에서 **파일 공유 감시 구성**을 클릭합니다.

   >[!TIP]
   >Windows Server 2016은 클라우드 감시를 지원합니다. 이 유형의 감시를 선택한 경우 파일 공유 감시가 필요하지 않습니다. 자세한 내용은 [장애 조치(Failover) 클러스터에 대한 클라우드 감시 배포](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness)를 참조하세요. 이 자습서에서는 이전 운영 체제에서 지원되는 파일 공유 감시를 사용합니다.

1. **파일 공유 감시 구성**, 사용자가 만든 hello 공유에 대 한 hello 패스를 입력 합니다. **다음**을 누릅니다.

1. Hello 설정을 확인 **확인**합니다. **다음**을 누릅니다.

1. **마침**을 클릭합니다.

hello 클러스터 코어 리소스 파일 공유 감시 구성 됩니다.

## <a name="enable-availability-groups"></a>가용성 그룹 사용

다음으로 hello를 사용 하도록 설정 **AlwaysOn 가용성 그룹** 기능입니다. 두 SQL Server에서 다음 단계를 수행합니다.

1. Hello에서 **시작** 화면을 시작 하며, **SQL Server 구성 관리자**합니다.
2. Hello 브라우저 트리에서 클릭 **SQL Server 서비스**, hello를 마우스 오른쪽 단추로 클릭 **SQL Server (MSSQLSERVER)** 서비스 마우스 클릭 **속성**합니다.
3. Hello 클릭 **AlwaysOn 고가용성** 탭 한 다음 선택 **AlwaysOn 가용성 그룹 사용**다음과 같이 합니다.

    ![AlwaysOn 가용성 그룹 사용](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/54-enableAlwaysOn.png)

4. **Apply**를 클릭합니다. 클릭 **확인** hello 팝업 대화 상자에서.

5. Hello SQL Server 서비스를 다시 시작 합니다.

다른 SQL Server hello에서 이러한 단계를 반복 합니다.

<!-----------------
## <a name="endpoint-firewall"></a>Open firewall for hello database mirroring endpoint

Each instance of SQL Server that participates in an Availability Group requires a database mirroring endpoint. This endpoint is a TCP port for hello instance of SQL Server that is used toosynchronize hello database replicas in hello Availability Groups on that instance.

On both SQL Servers, open hello firewall for hello TCP port for hello database mirroring endpoint.

1. On hello first SQL Server **Start** screen, launch **Windows Firewall with Advanced Security**.
2. In hello left pane, select **Inbound Rules**. On hello right pane, click **New Rule**.
3. For **Rule Type**, choose **Port**.
1. For hello port, specify TCP and choose an unused TCP port number. For example, type *5022* and click **Next**.

   >[!NOTE]
   >For this example, we're using TCP port 5022. You can use any available port.

5. In hello **Action** page, keep **Allow hello connection** selected and click **Next**.
6. In hello **Profile** page, accept hello default settings and click **Next**.
7. In hello **Name** page, specify a rule name, such as **Default Instance Mirroring Endpoint** in hello **Name** text box, then click **Finish**.

Repeat these steps on hello second SQL Server.
-------------------------->

## <a name="create-a-database-on-hello-first-sql-server"></a>Hello에 데이터베이스를 만드는 첫 번째 SQL Server

1. 시작 hello RDP 파일 toohello 도메인이 포함 된 첫 번째 SQL Server 계정 즉 sysadmin 소속 고정 서버 역할입니다.
1. SQL Server Management Studio를 열고 연결 toohello 첫 번째 SQL Server.
7. **개체 탐색기**에서 **데이터베이스**를 마우스 오른쪽 단추로 클릭하고 **새 데이터베이스**를 클릭합니다.
8. **데이터베이스 이름**에 **MyDB1**을 입력하고 **확인**을 클릭합니다.

### <a name="backupshare"></a> 백업 공유 만들기

1. 첫 번째 SQL Server에 hello **서버 관리자**, 클릭 **도구**합니다. **컴퓨터 관리**를 엽니다.

1. **공유 폴더**를 클릭합니다.

1. **공유**를 마우스 오른쪽 단추로 클릭하고 **새 공유...**를 클릭합니다.

   ![새 공유](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   사용 하 여 **공유 폴더 만들기 마법사** toocreate를 공유 합니다.

1. **폴더 경로**, 클릭 **찾아보기** 를 찾거나 hello 데이터베이스 백업 공유 폴더에 대 한 경로 만듭니다. **다음**을 누릅니다.

1. **이름, 설명 및 설정을** hello 공유 이름 및 경로 확인 합니다. **다음**을 누릅니다.

1. **공유 폴더 사용 권한**에서 **사용 권한 사용자 지정**을 설정합니다. **사용자 지정...**을 클릭합니다.

1. **사용 권한 사용자 지정**에서 **추가...**를 클릭합니다.

1. 두 서버 모두에 대 한 hello SQL Server 및 SQL Server 에이전트 서비스 계정에 모든 권한이 있는지 확인 합니다.

   ![새 공유](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/68-backupsharepermission.png)

1. **확인**을 클릭합니다.

1. **공유 폴더 사용 권한**에서 **마침**을 클릭합니다. **마침**을 다시 클릭합니다.  

### <a name="take-a-full-backup-of-hello-database"></a>전체 hello 데이터베이스의 백업을 수행합니다

Hello 새 데이터베이스 tooinitialize hello 로그 체인을 tooback이 필요합니다. Hello 새 데이터베이스의 백업을 더 이상 수행 하지 않으면 가용성 그룹에 포함할 수 없습니다.

1. **개체 탐색기**hello 데이터베이스를 마우스 오른쪽 단추로 너무 가리킨**작업 중... **, 클릭 **백업**합니다.

1. 클릭 **확인** tootake 전체 백업 toohello 기본 백업 위치입니다.

## <a name="create-hello-availability-group"></a>Hello 가용성 그룹 만들기
사용자는 이제 준비 tooconfigure 단계를 수행 하는 hello를 사용 하 여 가용성 그룹:

* Hello에 데이터베이스를 만드는 첫 번째 SQL Server.
* 전체 백업과 hello 데이터베이스의 트랜잭션 로그 백업을 모두
* 전체 복원 hello 및 hello로 SQL Server의 두 번째 로그 백업이 toohello **NORECOVERY** 옵션
* Hello 가용성 그룹 만들기 (**AG1**) 읽기 가능한 보조 복제본, 동기 커밋 및 자동 장애 조치와

### <a name="create-hello-availability-group"></a>Hello 가용성 그룹을 만듭니다.

1. 원격 데스크톱 세션 toohello에서 첫 번째 SQL Server. SSMS의 **개체 탐색기**에서 **AlwaysOn 고가용성**을 마우스 오른쪽 단추로 클릭하고 **새 가용성 그룹 마법사**를 클릭합니다.

    ![새 가용성 그룹 마법사 시작](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/56-newagwiz.png)

2. Hello에 **소개** 페이지 **다음**합니다. Hello에 **가용성 그룹 이름 지정** 페이지에서, 예를 들어 hello 가용성 그룹에 대 한 이름을 입력 **AG1**에 **가용성 그룹 이름**합니다. **다음**을 누릅니다.

    ![새 AG 마법사, AG 이름 지정](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/58-newagname.png)

3. Hello에 **데이터베이스 선택** 페이지 데이터베이스를 선택 하 고 클릭 **다음**합니다.

   >[!NOTE]
   >hello 의도 된 주 복제본에서 최소한 하나의 전체 백업을 수행 했으므로 hello 데이터베이스가 가용성 그룹에 대 한 hello 필수 구성 요소를 충족 합니다.

   ![새 AG 마법사, 데이터베이스 선택](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/60-newagselectdatabase.png)
4. Hello에 **복제본 지정** 페이지 **Add Replica**합니다.

   ![새 AG 마법사, 복제본 지정](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/62-newagaddreplica.png)
5. hello **tooServer 연결** 대화 상자가 나타납니다. 두 번째 서버 hello 형식 hello 이름 **서버 이름**합니다. **Connect**를 클릭합니다.

   Hello에 다시 **복제본 지정** 페이지에서 이제 표시 hello 두 번째 서버에 나열 된 **가용성 복제본**합니다. 다음과 같이 hello 복제본을 구성 합니다.

   ![새 AG 마법사, 복제본 지정(전체)](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/64-newagreplica.png)

6. 클릭 **끝점** toosee hello 데이터베이스 미러링 끝점이이 가용성 그룹에 대 한 합니다. 사용 하 여 hello hello을 설정할 때 사용 하는 동일한 포트 [데이터베이스 미러링 끝점에 대 한 방화벽 규칙](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall)합니다.

    ![새 AG 마법사, 초기 데이터 동기화 선택](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/66-endpoint.png)

8. Hello에 **초기 데이터 동기화 선택** 페이지 **전체** 공유 네트워크 위치를 지정 합니다. Hello 위치에 대 한 hello를 사용 하 여 [만든 백업 공유](#backupshare)합니다. 에 있는 경우 hello 예에서 **\\\\\<첫 번째 SQL Server\>\Backup\**합니다. **다음**을 누릅니다.

   >[!NOTE]
   >SQL Server의 첫 번째 인스턴스에 hello hello 데이터베이스의 전체 백업을 수행 하 고 toohello 두 번째 인스턴스를 복원 하는 전체 동기화 합니다. 대형 데이터베이스의 경우 전체 동기화는 시간이 오래 걸릴 수 있으므로 권장되지 않습니다. 수동으로 hello 데이터베이스의 백업을 수행 하 고 사용 하 여 복원 하 여이 시간을 줄일 수 `NO RECOVERY`합니다. Hello 데이터베이스를 복원 하는 경우 `NO RECOVERY` hello hello 가용성 그룹을 구성 하기 전에 SQL Server의 두 번째, 선택 **조인만**합니다. Hello 가용성 그룹을 구성한 후 tootake hello 백업 하려는 경우 선택 **초기 데이터 동기화 건너뛰기**합니다.

    ![새 AG 마법사, 초기 데이터 동기화 선택](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/70-datasynchronization.png)

9. Hello에 **유효성 검사** 페이지 **다음**합니다. 이 페이지에는 다음 이미지와 비슷한 toohello 같아야 합니다.

    ![새 AG 마법사, 유효성 검사](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/72-validation.png)

    >[!NOTE]
    >가용성 그룹 수신기를 구성 하지 않았기 때문에는 hello 수신기 구성에 대 한 경고입니다. Azure 가상 컴퓨터에 수신기를 만들면 hello hello Azure 부하 분산 장치를 만든 후 때문에이 경고를 무시할 수 있습니다.

10. Hello에 **요약** 페이지 **마침**, 다음 hello 마법사를 구성 하는 동안 잠시 기다려 hello 새 가용성 그룹입니다. Hello에 **진행률** 페이지에서 클릭할 수 있는 **자세한 내용을 보려면** tooview hello 진행 상황을 설명 합니다. Hello 마법사가 완료 되 면 hello 검사 **결과** 가용성 그룹을 hello 페이지 tooverify 성공적으로 만들었습니다.

     ![새 AG 마법사, 결과](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/74-results.png)
11. 클릭 **닫기** tooexit hello 마법사.

### <a name="check-hello-availability-group"></a>가용성 그룹 hello를 확인 합니다.

1. **개체 탐색기**에서 **AlwaysOn 고가용성**을 확장하고 **가용성 그룹**을 확장합니다. 이제이 컨테이너에 새 가용성 그룹을 hello 합니다. Hello 가용성 그룹을 마우스 오른쪽 단추로 클릭 하 고 클릭 **대시보드 표시**합니다.

   ![AG 대시보드 표시](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/76-showdashboard.png)

   프로그램 **AlwaysOn 대시보드** 비슷한 toothis 같아야 합니다.

   ![AG 대시보드](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/78-agdashboard.png)

   Hello 복제본, 각 복제본과 hello 동기화 상태의 hello 장애 조치 모드를 확인할 수 있습니다.

2. **장애 조치(Failover) 클러스터 관리자**에서 클러스터를 클릭합니다. **역할**을 선택합니다. hello 가용성 그룹 이름을 사용 하는 hello 클러스터에서 역할입니다. 수신기를 구성하지 않았기 때문에 해당 가용성 그룹은 클라이언트 연결에 대한 IP 주소가 없습니다. Azure 부하 분산 장치를 만든 후에 hello 수신기를 구성 합니다.

   ![장애 조치(Failover) 클러스터 관리자에서 AG](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/80-clustermanager.png)

   > [!WARNING]
   > Hello 장애 조치 클러스터 관리자에서에서 hello 가용성 그룹을 통해 toofail를 시도 하지 않습니다. 모든 장애 조치(Failover) 작업은 SSMS의 **AlwaysOn 대시보드** 에서 수행해야 합니다. 자세한 내용은 참조 [사용에 대 한 제한에는 가용성 그룹 장애 조치 클러스터 관리자 hello](https://msdn.microsoft.com/library/ff929171.aspx)합니다.
    >

이 시점에서 SQL Server의 두 인스턴스에서 복제와 함께 가용성 그룹을 갖게 됩니다. 인스턴스 간에 hello 가용성 그룹을 이동할 수 있습니다. 수신기 없기 때문에 아직 toohello 가용성 그룹을 연결할 수 없습니다. Azure 가상 컴퓨터의 hello 수신기 부하 분산 장치에 필요 합니다. hello 다음 단계는 Azure의 hello 부하 분산 장치 toocreate입니다.

<a name="configure-internal-load-balancer"></a>

## <a name="create-an-azure-load-balancer"></a>Azure Load Balancer 만들기

Azure Virtual Machines에서 SQL Server 가용성 그룹에는 부하 분산 장치가 필요합니다. hello 부하 분산 장치는 hello 가용성 그룹 수신기에 대 한 hello IP 주소를 보유합니다. 이 섹션에서는 toocreate hello 부하 분산 장치 hello Azure 포털에서에서 하는 방법을 요약 합니다.

1. Azure 포털 hello, 여기에서 SQL Server는 고 클릭 toohello 리소스 그룹 이동 **+ 추가**합니다.
2. **부하 분산 장치**를 검색합니다. Microsoft에서 게시 하는 hello 부하 분산 장치를 선택 합니다.

   ![장애 조치(Failover) 클러스터 관리자에서 AG](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/82-azureloadbalancer.png)

1.  **만들기**를 클릭합니다.
3. Hello 부하 분산 장치에 대 한 매개 변수 뒤 hello를 구성 합니다.

   | 설정 | 필드 |
   | --- | --- |
   | **Name** |예를 들어 hello 부하 분산 장치에 대 한 텍스트 이름을 사용 하 여 **sqlLB**합니다. |
   | **형식** |내부 |
   | **가상 네트워크** |Hello hello Azure 가상 네트워크 이름을 사용 합니다. |
   | **서브넷** |가상 컴퓨터를 hello hello 서브넷의 사용 하 여 hello 이름이입니다.  |
   | **IP 주소 할당** |정적 |
   | **IP 주소** |서브넷에서 사용 가능한 주소를 사용합니다. |
   | **구독** |사용 하 여 hello 동일 hello 가상 컴퓨터로 구독 합니다. |
   | **위치**: |사용 하 여 hello 동일 hello 가상 컴퓨터로 위치입니다. |

   Azure 포털 블레이드 hello 다음과 같이 표시 됩니다.

   ![부하 분산 장치 만들기](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/84-createloadbalancer.png)

1. 클릭 **만들기**, toocreate hello에 대 한 부하 분산 장치입니다.

tooconfigure hello 부하 분산 장치 백 엔드 풀 toocreate, probe, 및 집합 hello 부하 분산 규칙 해야 합니다. Hello Azure 포털에서에서이 수행 합니다.

### <a name="add-backend-pool"></a>백 엔드 풀 추가

1. Azure 포털 hello tooyour 가용성 그룹을 이동 합니다. Toorefresh hello 보기 toosee hello 새로 만든 부하 분산 장치를 할 수 있습니다.

   ![리소스 그룹의 부하 분산 장치 찾기](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/86-findloadbalancer.png)

1. Hello 부하 분산 장치를 클릭 하 고 **백 엔드 풀**를 클릭 하 고 **+ 추가**합니다. Hello 백 엔드 풀을 다음과 같이 설정 합니다.

   | 설정 | 설명 | 예제
   | --- | --- |---
   | **Name** | 텍스트 이름 입력 | SQLLBBE
   | **연결 대상** | 목록에서 선택 | 가용성 집합
   | **가용성 집합** | SQL Server Vm에 있는 hello 가용성 집합의 이름을 사용 하 여 | sqlAvailabilitySet |
   | **가상 컴퓨터** |두 hello Azure SQL Server VM 이름 | sqlserver-0, sqlserver-1

1. Hello 백 엔드 풀에 대 한 hello 이름을 입력 합니다.

1. **+가상 컴퓨터 추가**를 클릭합니다.

1. Hello 가용성 집합에 대 한 hello 가용성 집합에 SQL Server의 해당 hello를 선택 합니다.

1. 가상 컴퓨터에 대 한 hello SQL 서버를 둘 다를 포함 합니다. Hello 파일 공유 미러링 모니터 서버를 포함 하지 마십시오.

1. 클릭 **확인** toocreate hello 백 엔드 풀입니다.

### <a name="set-hello-probe"></a>집합 hello 프로브

1. Hello 부하 분산 장치를 클릭 하 고 **상태 프로브**를 클릭 하 고 **+ 추가**합니다.

1. 다음과 같이 hello 상태 프로브를 설정 합니다.

   | 설정 | 설명 | 예제
   | --- | --- |---
   | **Name** | 텍스트 | SQLAlwaysOnEndPointProbe |
   | **프로토콜** | TCP 선택 | TCP |
   | **포트** | 사용하지 않는 모든 포트 | 59999 |
   | **간격**  | hello 프로브 시간 간격 (초) 시도 |5 |
   | **비정상 임계값** | hello에 대 한 비정상으로 간주 하는 가상 컴퓨터 toobe 발생 해야 하는 연속 프로브 오류 수  | 2 |

1. 클릭 **확인** tooset hello 상태 검색 합니다.

### <a name="set-hello-load-balancing-rules"></a>Hello 부하 분산 규칙 설정

1. Hello 부하 분산 장치를 클릭 하 고 **부하 분산 규칙**를 클릭 하 고 **+ 추가**합니다.

1. Hello 부하 분산 규칙을 다음과 같이 설정 합니다.
   | 설정 | 설명 | 예제
   | --- | --- |---
   | **Name** | 텍스트 | SQLAlwaysOnEndPointListener |
   | **프런트 엔드 IP 주소** | 주소 선택 |Hello 부하 분산 장치를 만들 때 만들어지는 hello 주소를 사용 합니다. |
   | **프로토콜** | TCP 선택 |TCP |
   | **포트** | SQL Server 인스턴스에 hello hello 포트 사용 | 1433 |
   | **백 엔드 포트** | 이 필드는 부동 IP가 직접 서버 반환에 대해 설정된 경우 사용하지 않습니다. | 1433 |
   | **프로브** |hello 프로브에 대해 지정한 hello 이름 | SQLAlwaysOnEndPointProbe |
   | **세션 지속성** | 드롭다운 목록 | **없음** |
   | **유휴 시간 제한** | 분 tookeep TCP 연결을 열 수 | 4 |
   | **부동 IP(Direct Server Return)** | |사용 |

   > [!WARNING]
   > 직접 서버 반환은 만드는 동안 설정됩니다. 이는 변경할 수 없습니다.

1. 클릭 **확인** tooset hello 부하 분산 규칙입니다.

## <a name="configure-listener"></a>Hello 수신기 구성

다음 일 toodo hello tooconfigure hello 장애 조치 클러스터에 가용성 그룹 수신기입니다.

> [!NOTE]
> 이 자습서에서는 하나의 ILB IP와 함께 단일 수신기-toocreate 해결 하는 방법을 보여 줍니다. 하나 이상의 IP 주소를 사용 하 여 하나 이상의 수신기 참조 toocreate [Create Availability Group listener 및 부하 분산 장치 | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.
>
>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-listener-port"></a>수신기 포트 설정

SQL Server Management Studio에서 hello 수신기 포트를 설정 합니다.

1. SQL Server Management Studio를 시작 하 고 toohello 주 복제본에 연결 합니다.

1. 너무 이동**AlwaysOn 고가용성** | **가용성 그룹** | **가용성 그룹 수신기**합니다.

1. 이제 장애 조치 클러스터 관리자에서 만든 hello 수신기 이름이 표시 됩니다. Hello 수신기 이름을 마우스 오른쪽 단추로 클릭 하 고 클릭 **속성**합니다.

1. Hello에 **포트** 상자 이전 사용 $EndpointPort hello를 사용 하 여 hello 가용성 그룹 수신기에 대 한 hello 포트 번호를 지정 합니다 (1433 hello이 기본값 이었습니다)를 클릭 한 다음 **확인**합니다.

이제 Resource Manager 모드에서 실행 중인 Azure Virtual Machines의 SQL Server 가용성 그룹이 만들어졌습니다.

## <a name="test-connection-toolistener"></a>테스트 연결 toolistener

tootest hello 연결:

1. RDP tooa SQL 서버 hello에 있는 동일한 가상 네트워크 구성 요소, 않도록 지정 되었으나 자체 hello 복제 합니다. 사용할 수 있습니다 hello hello 클러스터의 다른 SQL Server.

1. 사용 하 여 **sqlcmd** 유틸리티 tootest hello 연결 합니다. 예를 들어 다음 스크립트는 hello 설정는 **sqlcmd** hello 수신기 Windows 인증을 통해 연결 toohello 주 복제본:

    ```
    sqlcmd -S <listenerName> -E
    ```

    Hello 수신기 포트를 사용 하는 이외의 경우 hello 기본 포트 (1433)를 hello 연결 문자열에 hello 포트를 지정 합니다. 예를 들어 hello 다음 sqlcmd 명령을 연결 tooa 수신기 포트 1435에서:

    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

hello SQLCMD 연결 toowhichever 인스턴스의 SQL Server 호스트 hello에 대 한 주 복제본을 자동으로 연결합니다.

> [!TIP]
> 지정한 hello 포트가 두 SQL Server의 hello 방화벽에서 열려 있는지 확인 합니다. 두 서버 hello 있습니다를 사용 하는 TCP 포트에 대 한 인바운드 규칙을 필요로 합니다. 자세한 내용은 [방화벽 규칙 추가 또는 편집](http://technet.microsoft.com/library/cc753558.aspx)을 참조하세요.
>
>



<!--**Notes**: *Notes provide just-in-time info: A Note is “by hello way” info, an Important is info users need toocomplete a task, Tip is for shortcuts. Don’t overdo*.-->


<!--**Procedures**: *This is hello second “step." They often include substeps. Again, use a short title that tells users what they’ll do*. *("Configure a new web project.")*-->

<!--**UI**: *Note hello format for documenting hello UI: bold for UI elements and arrow keys for sequence. (Ex. Click **File > New > Project**.)*-->

<!--**Screenshot**: *Screenshots really help users. But don’t include too many since they’re difficult toomaintain. Highlight areas you are referring tooin red.*-->

<!--**No. of steps**: *Make sure hello number of steps within a procedure is 10 or fewer. Seven steps is ideal. Break up long procedure logically.*-->


<!--**Next steps**: *Reiterate what users have done, and give them interesting and useful next steps so they want toogo on.*-->

## <a name="next-steps"></a>다음 단계

- [두 번째 가용성 그룹에서 IP 주소 tooa 부하 분산 장치 추가](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP)합니다.
