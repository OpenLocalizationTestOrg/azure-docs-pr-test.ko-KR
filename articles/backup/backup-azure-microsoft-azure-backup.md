---
title: "작업 부하 tooAzure Azure 백업 서버 tooback aaaUse | Microsoft Docs"
description: "Azure 백업 서버 tooprotect를 사용 하 여 또는 작업 toohello Azure 포털을 백업 합니다."
services: backup
documentationcenter: 
author: PVRK
manager: shivamg
editor: 
keywords: "Azure Backup Server; 워크로드 보호; 워크로드 백업"
ms.assetid: e7fb1907-9dc1-4ca1-8c61-50423d86540c
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/20/2017
ms.author: masaran;trinadhk;pullabhk;markgal
ms.openlocfilehash: a99b2919ffd44c6133960e3a935038a2bb1281c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-tooback-up-workloads-using-azure-backup-server"></a>Azure 백업 서버를 사용 하 여 워크 로드를 tooback 준비
> [!div class="op_single_selector"]
> * [Azure 백업 서버](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
>
>

이 문서에서는 설명 방법을 tooprepare Azure 백업 서버를 사용 하 여 워크 로드를 사용자 환경 tooback 합니다. Azure Backup Server로 Hyper-V VM, Microsoft SQL Server, SharePoint Server, 단일 콘솔의 Microsoft Exchange 및 Windows 클라이언트와 같은 응용 프로그램 워크로드를 보호할 수 있습니다.

> [!NOTE]
> Azure Backup Server는 이제 VMware VM을 보호하고 개선된 보안 기능을 제공할 수 있습니다. 아래; hello 섹션에 설명 된 대로 hello 제품을 설치 합니다. 최신 Azure 백업 에이전트 hello 및 업데이트 1을 적용 됩니다. Azure 백업 서버 VMware 서버 백업에 대해 자세히 toolearn hello 문서를 참조 하십시오. [VMware 서버를 사용 하 여 Azure 백업 서버 tooback](backup-azure-backup-server-vmware.md)합니다. 보안 기능에 대 한 toolearn 너무 참조[Azure 백업 보안 기능이 설명서](backup-azure-security-feature.md)합니다.
>
>

Azure의 VM과 같은 IaaS(Infrastructure as a Service) 작업을 보호할 수도 있습니다.

> [!NOTE]
> Azure에는 리소스를 만들고 작업하기 위한 두 가지 배포 모델인 [리소스 관리자와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)모델이 있습니다. 이 문서에서는 hello 리소스 관리자 모델을 사용 하 여 배포 된 Vm을 복원 하기 위한 hello 정보 및 절차를 제공 합니다.
>
>

Data Protection Manager (DPM)에서 azure 백업 서버 hello 작업 백업 기능을 상속합니다. 이 문서 연결 tooDPM 설명서 tooexplain hello의 일부 기능을 공유 합니다. Azure 백업 서버 hello 많이 공유 하는 경우 DPM와 동일한 기능을 합니다. Azure 백업 서버는 그렇지 않습니다 tootape, 백업 또는 System Center와 통합할 수 있습니다.

## <a name="1-choose-an-installation-platform"></a>1. 설치 플랫폼 선택
hello Azure 백업 서버 시작 및 실행 hello 첫 번째 단계는 Windows 서버를 tooset 합니다. 서버는 Azure 또는 온-프레미스에 있을 수 있습니다.

### <a name="using-a-server-in-azure"></a>Azure에서 서버 사용
Azure 백업 서버를 실행하기 위한 서버를 선택할 때 Windows Server 2012 R2 Datacenter의 갤러리 이미지로 시작하는 것이 좋습니다. hello 문서 [hello Azure 포털에서에서 첫 번째 Windows 가상 컴퓨터를 만들](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 하기 전에 Azure를 사용한 경험이 없는 경우에 azure에서 가상 컴퓨터를 권장 hello로 시작에 대 한 자습서를 제공 합니다. hello 최소 권장 요구 사항 hello 서버 가상 컴퓨터 (VM) 이어야 합니다: 2 코어 및 RAM이 3.5 g B와 a 2 표준입니다.

Azure 백업 서버를 사용하여 워크로드를 보호하는 데는 미묘한 많은 차이가 있습니다. hello 문서 [Install DPM Azure 가상 컴퓨터로](https://technet.microsoft.com/library/jj852163.aspx)를 통해 이러한 차이이 사소한에 설명 합니다. Hello 컴퓨터를 배포 하기 전에이 문서를 완전히 읽어 보세요.

### <a name="using-an-on-premises-server"></a>온-프레미스 서버 사용
Azure의 hello 기본 서버 toorun 하지 않으려면 hello 서버 Hyper-v VM, VMware VM 또는 실제 호스트에서 실행할 수 있습니다. hello는 hello 서버 하드웨어에 대 한 최소 요구 사항은 2 코어 및 4GB RAM 권장 합니다. hello 지원 운영 체제는 다음 표에 hello에 나열 됩니다.

| 운영 체제 | 플랫폼 | SKU |
|:--- | --- |:--- |
| Windows Server 2012 R2 및 최신 SP |64비트 |Standard, Datacenter, Foundation |
| Windows Server 2012 및 최신 SP |64비트 |Datacenter, Foundation, Standard |
| Windows Storage Server 2012 R2 및 최신 SP |64비트 |Standard, Workgroup |
| Windows Storage Server 2012 및 최신 SP |64비트 |Standard, Workgroup |

Windows Server 중복 제거를 사용 하 여 hello DPM 저장소 중복 제거 수 있습니다. [DPM 및 중복 제거](https://technet.microsoft.com/library/dn891438.aspx) 가 Hyper-V VM에 배포될 때 함께 작동하는 방법에 대해 자세히 알아보세요.

> [!NOTE]
> Azure 백업 서버는 단일 용도의 전용된 서버에서 설계 된 toorun입니다. Azure Backup Server를 다음 항목에 설치할 수 없습니다.
> - 도메인 컨트롤러로 실행하는 컴퓨터
> - 어떤 hello 응용 프로그램 서버 역할이 설치 된 컴퓨터
> - System Center Operations Manager 관리 서버인 컴퓨터
> - Exchange Server를 실행하는 컴퓨터
> - 클러스터의 한 노드인 컴퓨터

항상 Azure 백업 서버 tooa 도메인에 가입 합니다. Toomove hello 서버 tooa 다른 도메인을 계획 하는 경우 Azure 백업 서버를 설치 하기 전에 hello 서버 toohello 새 도메인에 가입 하는 것이 좋습니다. 배포 된 후 tooa 새 도메인 컴퓨터는 기존 Azure 백업 서버를 이동 *지원 되지 않습니다*합니다.

## <a name="2-recovery-services-vault"></a>2. Recovery Services 자격 증명 모음
TooAzure 백업 데이터를 전송 하거나 로컬로 보관할 연결 toobe tooAzure hello 소프트웨어에 필요 합니다. 보다 구체적인 toobe, hello Azure 백업 서버 컴퓨터 toobe 복구 서비스 자격 증명 모음에 등록 해야 합니다.

toocreate 복구 서비스 자격 증명 모음:

1. Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. Hello 허브 메뉴에서 클릭 **찾아보기** hello 리소스 목록에 입력 하 고 **복구 서비스**합니다. 입력을 시작할 때 hello 사용자 입력에 따라 필터를 나열 합니다. **복구 서비스 자격 증명 모음**을 클릭합니다.

    ![복구 서비스 자격 증명 모음 만들기 1단계](./media/backup-azure-microsoft-azure-backup/open-recovery-services-vault.png) <br/>

    복구 서비스 자격 증명 모음 hello 목록이 표시 됩니다.
3. Hello에 **복구 서비스 자격 증명 모음** 메뉴를 클릭 하 여 **추가**합니다.

    ![복구 서비스 자격 증명 모음 만들기 2단계](./media/backup-azure-microsoft-azure-backup/rs-vault-menu.png)

    hello 복구 서비스 자격 증명 모음에 블레이드에서 열립니다 tooprovide 묻는 **이름**, **구독**, **리소스 그룹**, 및 **위치**합니다.

    ![복구 서비스 자격 증명 모음 만들기 5단계](./media/backup-azure-microsoft-azure-backup/rs-vault-attributes.png)
4. 에 대 한 **이름**, 이름 tooidentify hello 자격 증명 모음을 입력 합니다. hello 이름이 필요 toobe 고유 hello Azure 구독에 대 한 합니다. 이름을 2~50자 사이로 입력합니다. 문자로 시작해야 하며, 문자, 숫자, 하이픈만 사용할 수 있습니다.
5. 클릭 **구독** toosee hello 사용 가능한 구독 목록입니다. 어떤 구독이 toouse 해야 할지 잘 모를 경우 hello 기본값을 사용 하 여 (또는 제안) 구독 합니다. 조직 계정이 여러 Azure 구독과 연결된 경우에만 여러 항목을 선택할 수 있습니다.
6. 클릭 **리소스 그룹** toosee 리소스 그룹의 사용 가능한 목록 hello 하거나 클릭 **새로** toocreate 새 리소스 그룹입니다. 리소스 그룹에 대한 전체 내용은 [Azure Resource Manager 개요](../azure-resource-manager/resource-group-overview.md)를 참조하세요.
7. 클릭 **위치** tooselect hello hello 자격 증명 모음에 대 한 지리적 영역입니다.
8. **만들기**를 클릭합니다. 복구 서비스 자격 증명 모음에 만든 toobe hello에 대 한 시간이 걸릴 수 있습니다. Hello hello 포털의 상단 오른쪽 영역에서 상태 알림 hello를 모니터링 합니다.
   자격 증명 모음을 만든 후 hello 포털에서 엽니다.

### <a name="set-storage-replication"></a>저장소 복제 설정
hello 저장소 복제 옵션 지역 중복 저장소와 로컬 중복 저장소는 toochoose가 있습니다. 기본적으로 사용자 자격 증명 모음에는 지역 중복 저장소가 있습니다. 이 자격 증명이 모음 자격 증명 기본 모음 이면 hello 저장소 옵션 집합 toogeo 중복 저장소를 둡니다. 오래 지속되지 않는 저렴한 옵션을 원하는 경우에는 로컬 중복 저장소를 선택합니다. 에 대해 자세히 알아보세요 [지리적 중복](../storage/common/storage-redundancy.md#geo-redundant-storage) 및 [로컬 중복](../storage/common/storage-redundancy.md#locally-redundant-storage) hello에 대 한 저장소 옵션 [Azure 저장소 복제 개요](../storage/common/storage-redundancy.md)합니다.

tooedit hello 저장소 복제 설정입니다.

1. 자격 증명 모음 tooopen hello 자격 증명 모음 대시보드 및 hello 설정 블레이드를 선택 합니다. 경우 hello **설정** 블레이드를 열고 하지 않는 **모든 설정을** hello 자격 증명 모음 대시보드에서.
2. Hello에 **설정** 블레이드에서 클릭 **백업 인프라** > **백업 구성** tooopen hello **백업구성** 블레이드입니다. Hello에 **백업 구성** 블레이드에서 자격 증명 모음에 대 한 hello 저장소 복제 옵션을 선택 합니다.

    ![백업 자격 증명 모음 목록](./media/backup-azure-vms-first-look-arm/choose-storage-configuration-rs-vault.png)

    자격 증명 모음에 대 한 hello 저장소 옵션을 선택한 후 hello 자격 증명 모음과 준비 tooassociate hello VM 됩니다. toobegin hello 연결 하면 검색 하 고 하는지 등록 hello Azure 가상 컴퓨터.

## <a name="3-software-package"></a>3. 소프트웨어 패키지
### <a name="downloading-hello-software-package"></a>Hello 소프트웨어 패키지를 다운로드합니다.
1. Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. 복구 서비스 자격 증명 모음 열고 이미 있는 경우 3 toostep을 진행 합니다. 복구 서비스 자격 증명 모음 열기를 갖지 않는 hello hello 허브 메뉴에서 Azure 포털에 있지만 클릭 **찾아보기**합니다.

   * Hello 리소스 목록에 입력 **복구 서비스**합니다.
   * Hello 목록이 필터링 됩니다 입력을 시작 하면 사용자의 입력에 기반 합니다. **복구 서비스 자격 증명 모음**이 표시되면 클릭합니다.

     ![복구 서비스 자격 증명 모음 만들기 1단계](./media/backup-azure-microsoft-azure-backup/open-recovery-services-vault.png)

     복구 서비스 자격 증명 모음 hello 목록이 표시 됩니다.
   * 복구 서비스 자격 증명 모음 hello 목록에서 자격 증명 모음을 선택 합니다.

     hello 선택한 자격 증명 모음 대시보드를 엽니다.

     ![자격 증명 모음 블레이드 열기](./media/backup-azure-microsoft-azure-backup/vault-dashboard.png)
3. hello **설정을** 블레이드 기본적으로 열립니다. 닫혀 있을 경우 클릭 하 여 **설정을** tooopen hello 설정 블레이드에서 합니다.

    ![자격 증명 모음 블레이드 열기](./media/backup-azure-microsoft-azure-backup/vault-setting.png)
4. 클릭 **백업** tooopen hello 시작 마법사.

    ![백업 시작](./media/backup-azure-microsoft-azure-backup/getting-started-backup.png)

    Hello에 **백업 시작** 열리면 블레이드 **백업 목표** 자동으로 선택 됩니다.

    ![백업-목표-기본-열기](./media/backup-azure-microsoft-azure-backup/getting-started.png)

5. Hello에 **백업 목표** 블레이드 hello에서 **여기서 작업이 실행 되는** 메뉴 선택 **온-프레미스**합니다.

    ![온-프레미스 및 목표 워크로드](./media/backup-azure-microsoft-azure-backup/backup-goals-azure-backup-server.png)

    Hello에서 **하 신 toobackup 원하는?** 드롭 다운 메뉴에서 Azure 백업 서버를 사용 하 여 tooprotect 하 고을 클릭 한 다음 선택 hello 작업 **확인**합니다.

    hello **백업 시작** 마법사 스위치 hello **준비 인프라** 작업 tooAzure tooback 옵션입니다.

   > [!NOTE]
   > 파일 및 폴더를 tooback만 하려는 경우 hello Azure 백업 에이전트를 사용 하 고 좋습니다 hello 지침 hello 문서에 [소개: 파일 및 폴더를 백업](backup-try-azure-backup-in-10-mins.md)합니다. Tooprotect를가 하는 경우 파일 및 폴더 또는 있습니다 tooexpand hello 보호 계획 보다 더 많은 필요 hello 이후에서 해당 작업 합니다.
   >
   >

    ![시작 마법사 변경](./media/backup-azure-microsoft-azure-backup/getting-started-prep-infra.png)

6. Hello에 **준비 인프라** 블레이드가 열리고 hello를 클릭 **다운로드** Azure 백업 서버를 설치 및 자격 증명 모음 다운로드에 대 한 링크입니다. Azure 백업 서버 toohello 복구 서비스 자격 증명 모음에 등록 하는 동안 hello 자격 증명 모음 자격 증명을 사용 합니다. hello 링크로 이동 하면 toohello 다운로드 센터 여기서 hello 소프트웨어 패키지를 다운로드할 수 있습니다.

    ![Azure 백업 서버에 대한 인프라 준비](./media/backup-azure-microsoft-azure-backup/azure-backup-server-prep-infra.png)

7. 모든 hello 파일을 선택 하 고 클릭 **다음**합니다. 다운로드 파일 hello Microsoft Azure 백업 다운로드 페이지에서 들어오는 hello 모든 및 위치에 있는 파일을 hello 모든 hello 동일한 폴더입니다.

    ![다운로드 센터 1](./media/backup-azure-microsoft-azure-backup/downloadcenter.png)

    이므로 hello 모든 hello 파일의 다운로드 크기 함께 > 3g, too60까지 걸릴 수 있으므로 10Mbps 다운로드 링크에서 hello에 대 한 분 toocomplete을 다운로드 합니다.

### <a name="extracting-hello-software-package"></a>Hello 소프트웨어 패키지를 추출합니다.
모든 hello 파일을 다운로드 한 후 클릭 **MicrosoftAzureBackupInstaller.exe**합니다. Hello을 시작 합니다. **Microsoft Azure 백업 설정 마법사** tooextract hello 설치 프로그램 파일을 사용자가 지정한 tooa 위치입니다. Hello 마법사를 계속 하 고 hello에서 클릭 **추출** toobegin hello 추출 프로세스 단추입니다.

> [!WARNING]
> 4GB 이상의 여유 공간이 필요한 tooextract hello 설치 파일입니다.
>
>

![Microsoft Azure 백업 설정 마법사](./media/backup-azure-microsoft-azure-backup/extract/03.png)

한 번 hello 추출 프로세스 완료를 확인 hello 상자 toolaunch hello 새로 추출한 *setup.exe* toobegin Microsoft Azure 백업 서버를 설치 하 고 hello에서 클릭 **마침** 단추 합니다.

### <a name="installing-hello-software-package"></a>Hello 소프트웨어 패키지 설치
1. 클릭 **Microsoft Azure 백업** toolaunch hello 설정 마법사입니다.

    ![Microsoft Azure 백업 설정 마법사](./media/backup-azure-microsoft-azure-backup/launch-screen2.png)
2. Hello 시작 화면에 hello 클릭 **다음** 단추입니다. 이렇게 하면 toohello *Prerequisite Checks* 섹션. 이 화면에서 클릭 **확인** toodetermine Azure 백업 서버에 대 한 hello 하드웨어 및 소프트웨어 필수 구성 요소가 충족 된 경우. 모든 필수 조건이 충족 되 면 해당 hello 컴퓨터 hello 요구 사항을 충족 하는지 나타내는 메시지가 표시 됩니다. Hello 클릭 **다음** 단추입니다.

    ![Azure 백업 서버 - 시작 및 필수 조건 확인](./media/backup-azure-microsoft-azure-backup/prereq/prereq-screen2.png)
3. Microsoft Azure 백업 서버에 SQL Server Standard 필요 하 고 hello Azure 백업 서버 설치 패키지 필요한 hello 적절 한 SQL Server 바이너리 번들로 묶은 제공 합니다. 새 Azure 백업 서버 설치를 시작할 때 hello 옵션을 선택 해야 **이 설치를 새 SQL Server 인스턴스 설치** hello 클릭 **확인 후 설치** 단추입니다. Hello 필수 구성 요소가 성공적으로 설치 되 면 클릭 **다음**합니다.

    ![Azure 백업 서버 - SQL 확인](./media/backup-azure-microsoft-azure-backup/sql/01.png)

    권장 사항 toorestart hello 컴퓨터와 함께 실패 한 경우 작업을 수행 하 고 클릭 **다시 확인**합니다.

   > [!NOTE]
   > Azure 백업 서버는 원격 SQL Server 인스턴스에서 작동하지 않습니다. Azure 백업 서버에서 사용 하 고 hello 인스턴스 toobe 로컬 필요 합니다.
   >
   >
4. Microsoft Azure 백업 서버 파일의 hello 설치에 대 한 위치를 입력 하 고 클릭 **다음**합니다.

    ![Microsoft Azure 백업 PreReq2](./media/backup-azure-microsoft-azure-backup/space-screen.png)

    hello 스크래치 위치는 tooAzure 백업에 대 한 요구 사항입니다. Hello 스크래치 위치는 hello 데이터의 5% 이상이 toobe toohello 클라우드 백업 계획을 확인 합니다. 디스크 보호에 대 한 별도 디스크 toobe hello 설치가 완료 된 후 구성 해야 합니다. 저장소 풀에 관련된 자세한 내용은 [저장소 풀 및 디스크 저장소 구성](https://technet.microsoft.com/library/hh758075.aspx)을 참조하세요.
5. 제한된 로컬 사용자 계정에 강력한 암호를 제공하고 **다음**을 클릭합니다.

    ![Microsoft Azure 백업 PreReq2](./media/backup-azure-microsoft-azure-backup/security-screen.png)
6. Toouse 것인지 선택 *Microsoft Update* 업데이트 및 클릭 toocheck **다음**합니다.

   > [!NOTE]
   > Windows Update에서는 Windows 및 Microsoft Azure 백업 서버과 같은 다른 제품에 대 한 보안 및 중요 업데이트는 업데이트를 tooMicrosoft 리디렉션됩니다 발생 하는 것이 좋습니다.
   >
   >

    ![Microsoft Azure 백업 PreReq2](./media/backup-azure-microsoft-azure-backup/update-opt-screen2.png)
7. 검토 hello *설정 요약* 클릭 **설치**합니다.

    ![Microsoft Azure 백업 PreReq2](./media/backup-azure-microsoft-azure-backup/summary-screen.png)
8. hello 설치 단계에서 발생합니다. 첫 번째 단계 hello hello에서에서 Microsoft Azure 복구 서비스 에이전트는 hello 서버에 설치 됩니다. hello 마법사는 또한 인터넷 연결을 확인합니다. 인터넷 연결을 사용할 수 있는 경우 설치를 계속 진행할 수 없으면 tooprovide 프록시 세부 정보 tooconnect toohello 인터넷 필요.

    hello 다음 단계는 tooconfigure hello Microsoft Azure 복구 서비스 에이전트입니다. Hello 구성의 일부로 해야 tooprovide 자격 증명 모음 자격 증명 tooregister hello 컴퓨터 toohello 복구 서비스 자격 증명 모음입니다. 또한 Azure와 고객의 프레미스 간에 전송 되는 암호 tooencrypt/암호 해독 hello 데이터를 제공 합니다. 자동으로 암호를 생성하거나 최소 16자인 고유의 암호를 제공할 수 있습니다. Hello 에이전트 구성 될 때까지 hello 마법사를 계속 합니다.

    ![Azure 백업 서버 PreReq2](./media/backup-azure-microsoft-azure-backup/mars/04.png)
9. Hello Microsoft Azure 백업 서버를 등록 성공적으로 완료 되 면 hello 전반적인 설치 마법사 진행 toohello 설치 하 고 SQL Server 및 hello Azure 백업 서버 구성 요소 구성 됩니다. Hello SQL Server 구성 요소 설치가 완료 되 면 hello Azure 백업 서버 구성 요소가 설치 됩니다.

    ![Azure Backup 서버](./media/backup-azure-microsoft-azure-backup/final-install/venus-installation-screen.png)

Hello 설치 단계 완료 되 면 hello 제품의 바탕 화면 아이콘 만들어집니다도 합니다. Hello 아이콘 toolaunch hello 제품을 두 번 클릭 합니다.

### <a name="add-backup-storage"></a>백업 저장소 추가
hello 첫 번째 백업 복사본은 연결 된 저장소 toohello Azure 백업 서버 컴퓨터에 유지 됩니다. 디스크 추가에 대한 자세한 내용은 [저장소 풀 및 디스크 저장소 구성](https://technet.microsoft.com/library/hh758075.aspx)을 참조하세요.

> [!NOTE]
> Toosend 데이터 tooAzure를 계획 하는 경우에 tooadd 백업 저장소가 필요 합니다. Azure 백업 서버의 현재 아키텍처 hello hello Azure 백업 자격 증명 모음 보유 hello *두 번째* hello 로컬 저장소 hello 첫 번째 (및 필수) 백업 복사본을 보유 하는 동안 hello 데이터의 복사본입니다.
>
>

## <a name="4-network-connectivity"></a>4. 네트워크 연결
Azure 백업 서버 제품 toowork hello에 대 한 연결 toohello Azure 백업 서비스를 성공적으로 필요합니다. toovalidate hello 컴퓨터 hello 연결 tooAzure에 있는지 여부를 사용 하 여 hello ```Get-DPMCloudConnection``` hello Azure 백업 서버 PowerShell 콘솔에서 cmdlet. 경우 hello hello cmdlet의 출력이 TRUE로 연결, 다른 연결이 없습니다.

Hello에 동시 hello Azure 구독 toobe 정상 상태에 있어야합니다. 구독 및 toomanage hello 상태 toofind 것 toohello 로그인 [구독 포털](https://account.windowsazure.com/Subscriptions)합니다.

Hello Azure 구독 및 hello Azure 연결의 hello 상태를 확인 했으면 hello 영향 아웃 toofind 아래 hello 표 제공 하는 hello 백업/복원 기능에 사용할 수 있습니다.

| 연결 상태 | Azure 구독 | TooAzure 백업 | Toodisk 백업 | Azure에서 복구 | 디스크에서 복구 |
| --- | --- | --- | --- | --- | --- |
| 연결됨 |Active |허용됨 |허용됨 |허용됨 |허용됨 |
| 연결됨 |만료됨 |중지됨 |중지됨 |허용됨 |허용됨 |
| 연결됨 |프로비전 해제됨 |중지됨 |중지됨 |중지되고 Azure 복구 지점 삭제됨 |중지됨 |
| 손실된 연결 > 15일 |Active |중지됨 |중지됨 |허용됨 |허용됨 |
| 손실된 연결 > 15일 |만료됨 |중지됨 |중지됨 |허용됨 |허용됨 |
| 손실된 연결 > 15일 |프로비전 해제됨 |중지됨 |중지됨 |중지되고 Azure 복구 지점 삭제됨 |중지됨 |

### <a name="recovering-from-loss-of-connectivity"></a>연결 끊김 복구
방화벽 또는 프록시 액세스 tooAzure를 방해 하는 경우 도메인 주소 hello 방화벽/프록시 프로필에 따라 toowhitelist hello가 필요 합니다.

* www.msftncsi.com
* \*.Microsoft.com
* \*.WindowsAzure.com
* \*.microsoftonline.com
* \*.windows.net

연결 tooAzure에 대 한 복원된 toohello Azure 백업 서버 컴퓨터를 수행한 후에 수행할 수 있는 hello 작업 hello Azure 구독 상태에 의해 결정 됩니다. 위의 hello 테이블 hello 컴퓨터 "연결"을 허용 하는 hello 작업에 대 한 세부 정보를 포함 합니다.

### <a name="handling-subscription-states"></a>구독 상태 처리
Azure 구독에서 가능한 tootake는는 *만료 됨* 또는 *Deprovisioned* 상태 toohello *활성* 상태입니다. 그러나이 일부 영향에 hello 제품 동작 hello 상태가 아닌 동안 *활성*:

* A *Deprovisioned* 구독 프로 비전이 해제 되는 기간에 hello에 대 한 기능을 손실 합니다. 선반에 *활성*, 백업/복원의 hello 제품 기능 다시 되 합니다. 또한 hello hello 로컬 디스크에 백업 데이터는 충분히 긴 보존 기간으로 유지 한 경우으로 검색할 수 있습니다. 그러나 Azure의 hello 백업 데이터는 hello hello 시작 되 면 영구적으로 손실 *Deprovisioned* 상태입니다.
* *만료됨* 구독은 다시 *활성* 상태로 되기 전까지 기능을 상실합니다. Hello 구독 하는 모든 백업은 hello 기간 중 예약 된 *만료 됨* 실행 되지 것입니다.

## <a name="troubleshooting"></a>문제 해결
Microsoft Azure 백업 서버 hello 설치 단계 (또는 백업 또는 복원) 하는 동안 오류와 함께 실패 하는 경우 참조 toothis [오류 코드 문서](https://support.microsoft.com/kb/3041338) 자세한 정보에 대 한 합니다.
너무 참조할 수도 있습니다[Azure 백업 관련 Faq](backup-azure-backup-faq.md)

## <a name="next-steps"></a>다음 단계
에 대 한 자세한 정보를 얻을 수 [DPM을 위한 환경 준비](https://technet.microsoft.com/library/hh758176.aspx) hello Microsoft TechNet 사이트에서. 또한 여기에는 Azure 백업 서버를 배포 및 사용하는 데 지원되는 구성에 대한 정보도 포함되어 있습니다.

이러한 문서 toogain Microsoft Azure 백업 서버를 사용 하는 작업 보호에 대 한 깊은 이해가 사용할 수 있습니다.

* [SQL Server 백업](backup-azure-backup-sql.md)
* [SharePoint 서버 백업](backup-azure-backup-sharepoint.md)
* [대체 서버 백업](backup-azure-alternate-dpm-server.md)
