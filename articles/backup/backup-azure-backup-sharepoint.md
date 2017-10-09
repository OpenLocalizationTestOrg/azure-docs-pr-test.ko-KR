---
title: "SharePoint 팜 tooAzure의 aaaDPM/Azure 백업 서버 보호 | Microsoft Docs"
description: "이 문서에서는 SharePoint 팜 tooAzure의 DPM/Azure 백업 서버 보호 개요"
services: backup
documentationcenter: 
author: adigan
manager: Nkolli1
editor: 
ms.assetid: e0c0c252-dc1d-4072-b777-7222c13950b0
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: adigan;giridham;jimpark;trinadhk;markgal
ms.openlocfilehash: 726d59320b8d9f14b38e0f041308019eebcfb77b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-sharepoint-farm-tooazure"></a>SharePoint 팜 tooAzure 백업
SharePoint 백업 팜에 tooMicrosoft Azure 많은 hello에서 System Center Data Protection Manager (DPM)를 사용 하 여 다른 데이터 소스를 백업 하는 동일한 방식으로 합니다. Azure 백업에서는 손쉽게 hello 백업 일정 toocreate 매일, 매주, 매월 또는 매년 백업 지점 및 다양 한 백업 지점에 대 한 보존 정책 옵션을 제공 합니다. DPM에서는 빠른 복구 시간 목표 (RTO)에 대 한 hello 기능 toostore 로컬 디스크 복사본을 제공 하 고 toostore tooAzure 경제적이 고, 장기 보존에 대 한 복사 합니다.

## <a name="sharepoint-supported-versions-and-related-protection-scenarios"></a>SharePoint가 지원하는 버전 및 관련 보호 시나리오
DPM에 대 한 azure 백업을 hello 다음 시나리오를 지원 합니다.

| 워크로드 | 버전 | SharePoint 배포 | DPM 배포 유형 | DPM - System Center 2012 R2 | 보호 및 복구 |
| --- | --- | --- | --- | --- | --- |
| SharePoint |SharePoint 2013, SharePoint 2010, SharePoint 2007, SharePoint 3.0 |SharePoint는 물리적 서버 또는 하이퍼-V/VMware 가상 컴퓨터로 배포됨  <br> -------------- <br> SQL AlwaysOn |물리적 서버 또는 온-프레미스 Hyper-v 가상 컴퓨터 |업데이트 롤업 5에서 백업 tooAzure 지원 |SharePoint 팜 보호 복구 옵션: 복구 팜, 데이터베이스, 및 파일 또는 디스크 복구 지점의 목록 항목   Azure 복구 지점에서 팜 및 데이터베이스 복구 |

## <a name="before-you-start"></a>시작하기 전에
몇 가지 방법으로 SharePoint 팜 tooAzure를 백업 하기 전에 tooconfirm 필요 합니다.

### <a name="prerequisites"></a>필수 조건
계속 진행 하기 전에 모든 hello가 충족 되는지 확인 [Microsoft Azure 백업을 사용 하기 위한 필수 구성 요소](backup-azure-dpm-introduction.md#prerequisites) tooprotect 작업 합니다. 필수 구성 요소에 대 한 일부 작업은 같습니다.: 백업 자격 증명 모음 만들기, 자격 증명 모음 자격 증명을 다운로드, Azure 백업 에이전트를 설치 및 DPM/Azure 백업 서버 hello 자격 증명 모음에 등록 합니다.

### <a name="dpm-agent"></a>DPM 에이전트
SharePoint를 실행 하는 hello 서버, SQL Server를 실행 하는 hello 서버 및 hello SharePoint 팜에 속하는 다른 모든 서버에 hello DPM 에이전트를 설치 해야 합니다. 방법에 대 한 자세한 내용은 hello 보호 에이전트를 tooset 참조 [보호 에이전트 설치](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx)합니다.  hello 한 가지 예외는 단일 웹 WFE (프런트 엔드) 서버에만 hello 에이전트를 설치 한다는 점입니다. DPM 보호에 대 한 hello 진입점으로 하나의 WFE 서버만 tooserve hello 에이전트가 필요합니다.

### <a name="sharepoint-farm"></a>Sharepoint 팜
Hello 팜의 모든 10 백만 항목에 대 한 최소 2GB의은 hello DPM 폴더가 있는 hello 볼륨에 공간 이어야 합니다. 이 공간은 카탈로그를 생성하는 데 필요 합니다. DPM toorecover 특정 항목 (사이트 모음, 사이트, 목록, 문서 라이브러리, 폴더, 개별 문서 및 목록 항목)에 대 한 카탈로그를 생성할 hello Url 각 콘텐츠 데이터베이스에 포함 된 목록을 만듭니다. Hello에 hello 복구 가능한 항목 창에서 Url hello 목록을 볼 수 있습니다 **복구** 작업 DPM 관리자 콘솔의 영역입니다.

### <a name="sql-server"></a>SQL Server
DPM은 LocalSystem 계정으로 실행됩니다. SQL Server 데이터베이스를 tooback, DPM SQL Server를 실행 하는 hello 서버에 대 한 해당 계정에 대 한 sysadmin 권한이 필요 합니다. NT AUTHORITY\SYSTEM을 너무 설정*sysadmin* 하기 전에 SQL Server를 실행 하는 hello 서버를 백업 합니다.

Hello SharePoint 팜에 SQL Server 데이터베이스를 SQL Server 별칭으로 구성 된 경우, DPM에서 보호할 hello 프런트 엔드 웹 서버 hello SQL Server 클라이언트 구성 요소를 설치 합니다.

### <a name="sharepoint-server"></a>SharePoint Server
성능은 SharePoint 팜의 크기와 같은 여러 요인에 따라 달라지지만, 일반 지침에 의하면 DPM 서버 하나가 25TB SharePoint 팜을 보호할 수 있습니다.

### <a name="dpm-update-rollup-5"></a>DPM 업데이트 롤업 5
SharePoint 팜 tooAzure toobegin 보호 해야 tooinstall DPM 업데이트 롤업 5 이상. 업데이트 롤업 5는 SQL AlwaysOn을 사용 하 여 hello 팜이 구성 되어 있으면 SharePoint 팜 tooAzure hello 기능 tooprotect를 제공 합니다.
자세한 내용은 블로그 게시물을 도입 하는 hello [DPM 업데이트 롤업 5](http://blogs.technet.com/b/dpm/archive/2015/02/11/update-rollup-5-for-system-center-2012-r2-data-protection-manager-is-now-available.aspx)

### <a name="whats-not-supported"></a>지원 되지않는 사항
* SharePoint 팜을 보호하는 DPM은 검색 인덱스 또는 응용 프로그램 서비스 데이터베이스를 보호하지 않습니다. 개별적으로 이러한 데이터베이스의 tooconfigure hello 보호를 해야 합니다.
* DPM은 스케일 아웃 파일 서버(SOFS) 공유에 호스트되는 SharePoint SQL Server 데이터베이스의 백업을 제공하지 않습니다.

## <a name="configure-sharepoint-protection"></a>SharePoint 보호 구성
사용 하 여 hello SharePoint VSS 기록기 서비스 (WSS 기록기 서비스)를 구성 해야 DPM tooprotect SharePoint를 사용 하려면 먼저 **ConfigureSharePoint.exe**합니다.

찾을 수 있습니다 **ConfigureSharePoint.exe** hello 프런트 엔드 웹 서버 hello [DPM 설치 경로] \bin 폴더에 있습니다. 이 도구는 hello SharePoint 팜에 대 한 hello 자격 증명으로 hello 보호 에이전트를 제공합니다. 단일 WFE 서버에서 실행합니다. WFE 서버가 여러 개인 경우, 보호 그룹을 구성할 때 하나만 선택합니다.

### <a name="tooconfigure-hello-sharepoint-vss-writer-service"></a>tooconfigure hello SharePoint VSS 기록기 서비스
1. 명령 프롬프트에서 hello WFE 서버에서 이동 너무 [DPM 설치 위치] \bin\
2. ConfigureSharePoint -EnableSharePointProtection을 입력합니다.
3. Hello 팜 관리자 자격 증명을 입력 합니다. 이 계정은 hello hello WFE 서버에서 로컬 관리자 그룹의 구성원 이어야 합니다. 팜 관리자에 게 다음 권한을 hello WFE 서버에서 로컬 관리자가 부여 hello 않다면,
   * Hello WSS_Admin_WPG 그룹 모든 권한 toohello DPM 폴더 (% Program Files%\Microsoft Data Protection Manager\DPM)에 권한을 부여 합니다.
   * Hello WSS_Admin_WPG 그룹 읽기 액세스 toohello DPM 레지스트리 키 (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager)을 부여 합니다.

> [!NOTE]
> Hello SharePoint 팜 관리자 자격 증명이 변경 될 때마다 toorerun ConfigureSharePoint.exe 필요 합니다.
> 
> 

## <a name="back-up-a-sharepoint-farm-by-using-dpm"></a>DPM을 사용하여 SharePoint 팜 백업
DPM과 hello 이전에 설명 된 대로 SharePoint 팜 구성 하 고 나면 SharePoint DPM에서 보호할 수 있습니다.

### <a name="tooprotect-a-sharepoint-farm"></a>SharePoint 팜에 tooprotect
1. Hello에서 **보호** hello DPM 관리자 콘솔의 탭을 클릭 **새로**합니다.
    ![새 보호 탭](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)
2. Hello에 **보호 그룹 종류 선택** hello 페이지 **새 보호 그룹 만들기** 마법사, 선택 **서버**, 클릭 하 고 **다음** .
   
    ![선택하는 보호 그룹 종류](./media/backup-azure-backup-sharepoint/select-protection-group-type.png)
3. Hello에 **그룹 구성원 선택** 화면, 누르고 원하는 tooprotect hello SharePoint 서버에 대 한 확인란을 선택 하는 hello **다음**합니다.
   
    ![그룹 구성원 선택](./media/backup-azure-backup-sharepoint/select-group-members2.png)
   
   > [!NOTE]
   > Hello DPM 에이전트 설치와 함께 hello 서버 hello 마법사에서 볼 수 있습니다. 또한 DPM에서는 해당 구조를 보여줍니다. ConfigureSharePoint.exe를 실행 하기 때문에 DPM hello SharePoint VSS 기록기 서비스와 해당 SQL Server 데이터베이스와 통신 하 고 hello SharePoint 팜 구조를 인식, hello 콘텐츠 데이터베이스 및 해당 항목에 연결 합니다.
   > 
   > 
4. Hello에 **데이터 보호 방법 선택** 페이지의 hello hello 이름을 입력 **보호 그룹**, 원하는 선택 *보호 방법을*합니다. **다음**을 누릅니다.
   
    ![데이터 보호 방법 선택](./media/backup-azure-backup-sharepoint/select-data-protection-method1.png)
   
   > [!NOTE]
   > hello 디스크 보호 방법 toomeet 짧은 복구 시간 목표를 수 있습니다. Azure는 경제적이 고, 장기 보호 비교 대상 tootapes입니다. 자세한 내용은 참조 [사용 하 여 Azure 백업 tooreplace 테이프 인프라](https://azure.microsoft.com/documentation/articles/backup-azure-backup-cloud-as-tape/)
   > 
   > 
5. Hello에 **단기 목표 지정** 페이지에서 원하는 **보존 범위** 백업을 toooccur 하려는 경우를 식별 합니다.
   
    ![단기 목표 지정](./media/backup-azure-backup-sharepoint/specify-short-term-goals2.png)
   
   > [!NOTE]
   > 때문에 복구 가장 자주 5 일 보다 작은 데이터에 필요한, म 디스크에 5 일의 보존 범위를 선택 하 고이 예제에 대 한 비-프로덕션 시간 동안 발생 하는 hello 백업 보장 합니다.
   > 
   > 
6. Hello 보호 그룹에 할당 된 hello 저장소 풀 디스크 공간을 검토 하 고 클릭 하 고 **다음**합니다.
7. 모든 보호 그룹에 대해 DPM 디스크 공간 toostore 할당 하 고 복제본을 관리 합니다. 이 시점에서 DPM hello 선택한 데이터의 복사본을 만들어야 합니다. 선택 방법 및 시기를 만든 hello 복제본을 클릭 한 다음 **다음**합니다.
   
    ![복제본 만들기 방법 선택](./media/backup-azure-backup-sharepoint/choose-replica-creation-method.png)
   
   > [!NOTE]
   > 네트워크 트래픽에 영향을 받지 않습니다, 있는지 toomake 프로덕션 시간 외 시간을 선택 합니다.
   > 
   > 
8. DPM은 hello 복제본에 일관성 검사를 수행 하 여 데이터 무결성을 보장 합니다. 사용할 수 있는 두 가지 옵션이 있습니다. 정의한 일정 toorun 일관성 검사, 또는 DPM이 일관 되지 않을 때마다 hello 복제본에서 자동으로 일관성 확인을 실행할 수 있습니다. 원하는 옵션을 선택하고 **다음**을 클릭합니다.
   
    ![일관성 확인](./media/backup-azure-backup-sharepoint/consistency-check.png)
9. Hello에 **온라인 보호 데이터 지정** hello SharePoint 팜에 tooprotect를 원하고 클릭 한 다음 페이지에서 **다음**합니다.
   
    ![DPM SharePoint Protection1](./media/backup-azure-backup-sharepoint/select-online-protection1.png)
10. Hello에 **온라인 백업 일정 지정** 페이지 원하는 일정을 선택 하 고 클릭 **다음**합니다.
    
    ![Online_backup_schedule](./media/backup-azure-backup-sharepoint/specify-online-backup-schedule.png)
    
    > [!NOTE]
    > DPM 서로 다른 시간에 최대 두 개의 일별 백업 tooAzure 제공합니다. Azure 백업 hello를 사용 하 여 최고 및 사용량이 적은 시간에 백업에 사용할 수 있는 WAN 대역폭 양을 제어할 수 [Azure 백업 네트워크 제한](https://azure.microsoft.com/en-in/documentation/articles/backup-configure-vault/#enable-network-throttling)합니다.
    > 
    > 
11. Hello hello에서 선택한 백업 일정에 따라 **온라인 보존 정책 지정** 매일, 매주, 매월 및 매년 백업 지점에 대 한 보존 정책 선택 hello 페이지입니다.
    
    ![Online_retention_policy](./media/backup-azure-backup-sharepoint/specify-online-retention.png)
    
    > [!NOTE]
    > DPM은 다른 백업 지점에 대해 다른 보전 정책을 사용하는 조부-아버지-아들 보존 체계를 사용합니다.
    > 
    > 
12. 비슷한 toodisk 초기 참조 지점 복제 데이터베이스를 Azure에서 만든 toobe가 필요 합니다. 사용자 기본 설정된 옵션 toocreate 초기 백업 복사본이 tooAzure를 선택한 다음 클릭 **다음**합니다.
    
    ![Online_replica](./media/backup-azure-backup-sharepoint/online-replication.png)
13. Hello에서 선택한 설정을 검토 **요약** 페이지를 선택한 다음 클릭 **그룹 만들기**합니다. Hello 보호 그룹을 만든 후 성공 메시지가 나타납니다.
    
    ![요약](./media/backup-azure-backup-sharepoint/summary.png)

## <a name="restore-a-sharepoint-item-from-disk-by-using-dpm"></a>DPM을 사용하여 디스크에서 SharePoint 항목 복원
다음 예제는 hello에서 hello *SharePoint 복구 항목* 실수로 삭제 하 고 복구 toobe 필요 합니다.
![DPM SharePoint Protection4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)

1. 열기 hello **DPM 관리자 콘솔**합니다. DPM에서 보호 되는 모든 SharePoint 팜 hello에 표시 된 **보호** 탭 합니다.
   
    ![DPM SharePoint Protection3](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection4.png)
2. toobegin toorecover hello 항목을 선택 하는 hello **복구** 탭 합니다.
   
    ![DPM SharePoint Protection5](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection6.png)
3. 복구 지점 범위 내에서 와일드카드 기반 검색을 사용하여 *SharePoint 항목을 복구할* SharePoint를 검색합니다.
   
    ![DPM SharePoint Protection6](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection7.png)
4. Hello 검색 결과에서 hello 적절 한 복구 지점을 선택 hello 항목을 마우스 오른쪽 단추로 클릭 하 고 다음 선택 **복구**합니다.
5. 다양 한 복구 지점을 찾아보거나 수 있고 데이터베이스 또는 항목 toorecover 선택 수도 있습니다. 선택 **날짜 > 복구 시간**를 선택한 후 올바른 hello **데이터베이스 > SharePoint 팜에 > 복구 지점 > 항목**합니다.
   
    ![DPM SharePoint Protection7](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection8.png)
6. Hello 항목을 마우스 오른쪽 단추로 클릭 한 다음 선택 **복구** tooopen hello **복구 마법사**합니다. **다음**을 누릅니다.
   
    ![복구 선택 사항 확인](./media/backup-azure-backup-sharepoint/review-recovery-selection.png)
7. Hello 유형의 recovery tooperform를 선택 하 고 클릭 한 다음 선택 **다음**합니다.
   
    ![복구 유형](./media/backup-azure-backup-sharepoint/select-recovery-type.png)
   
   > [!NOTE]
   > 선택 hello **toooriginal 복구** hello의 예제는 hello 항목 toohello 원래 SharePoint 사이트를 복구 합니다.
   > 
   > 
8. 선택 hello **복구 프로세스** toouse 되도록 합니다.
   
   * 선택 **복구 팜을 사용 하지 않고 복구** hello SharePoint 팜에 변경 되지 않은 경우 및 해당 하는 지점 hello 복구 동일 hello 복원 하는 중입니다.
   * 선택 **복구 팜을 사용 하 여 복구** hello SharePoint 팜에 hello 복구 지점이 만들어진 후 변경 된 경우.
     
     ![복구 프로세스](./media/backup-azure-backup-sharepoint/recovery-process.png)
9. 준비 SQL Server 인스턴스 위치 toorecover hello 데이터베이스를 일시적으로 제공 하 고 hello DPM 서버와 SharePoint toorecover hello 항목을 실행 하는 hello 서버를 준비 하는 파일 공유를 제공 합니다.
   
    ![스테이징 위치 1](./media/backup-azure-backup-sharepoint/staging-location1.png)
   
    DPM은 hello SharePoint 항목 toohello 임시 SQL Server 인스턴스를 호스팅하는 hello 콘텐츠 데이터베이스를 연결 합니다. Hello 콘텐츠 데이터베이스에서 DPM 서버 hello hello 항목을 복구 하 고 hello 스테이징 hello DPM 서버에서 파일 위치에 저장 합니다. hello 이제 hello DPM 서버의 위치를 준비 하는 hello에 있는 복구 항목 필요 내보낸 toobe toohello hello SharePoint 팜에서 위치를 준비 합니다.
   
    ![스테이징 Location2](./media/backup-azure-backup-sharepoint/staging-location2.png)
10. 선택 **복구 옵션 지정**, 및 보안 설정을 toohello SharePoint 팜에 적용 또는 hello 복구 지점의 hello 보안 설정을 적용 합니다. **다음**을 누릅니다.
    
    ![복구 옵션](./media/backup-azure-backup-sharepoint/recovery-options.png)
    
    > [!NOTE]
    > Toothrottle hello 네트워크 대역폭 사용을 선택할 수 있습니다. 이 영향 toohello 프로덕션 서버 프로덕션 많은 시간을 최소화합니다.
    > 
    > 
11. Hello 요약 정보를 검토 한 다음 클릭 **복구** hello 파일의 toobegin 복구 합니다.
    
    ![복구 요약](./media/backup-azure-backup-sharepoint/recovery-summary.png)
12. 이제 선택 하는 hello **모니터링** hello 탭 **DPM 관리자 콘솔** tooview hello **상태** hello 복구 합니다.
    
    ![복구 상태](./media/backup-azure-backup-sharepoint/recovery-monitoring.png)
    
    > [!NOTE]
    > 이제 hello 파일 복원 되었습니다. Hello SharePoint 사이트 toocheck hello 복원 파일을 새로 고칠 수 있습니다.
    > 
    > 

## <a name="restore-a-sharepoint-database-from-azure-by-using-dpm"></a>DPM을 사용하여 Azure에서 SharePoint 데이터베이스 복원
1. SharePoint 콘텐츠 데이터베이스 toorecover 다양 한 복구 지점 (이전에 표시)으로, toorestore 원하는 hello 복구 지점을 선택 합니다.
   
    ![DPM SharePoint Protection8](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection9.png)
2. Hello SharePoint 복구 지점 tooshow hello 사용 가능한 SharePoint 카탈로그 정보를 두 번 클릭 합니다.
   
   > [!NOTE]
   > Azure에서 장기 보존을 위해 hello SharePoint 팜 보호 되 면 카탈로그 비워진 (메타 데이터) 이므로 hello DPM 서버에서 사용할 수 있는 합니다. 결과적으로, 지정 시간 SharePoint 콘텐츠 데이터베이스 복구 toobe, 필요할 때마다 있습니다 toocatalog hello SharePoint 팜에 다시 필요 합니다.
   > 
   > 
3. **카탈로그 다시 만들기**를 클릭합니다.
   
    ![DPM SharePoint Protection10](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection12.png)
   
    hello **클라우드 카탈로그를 다시** 상태 창이 열립니다.
   
    ![DPM SharePoint Protection11](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection13.png)
   
    Hello 상태가 너무 변경 카탈로그 만들기를 완료 한 후*성공*합니다. **닫기**를 클릭합니다.
   
    ![DPM SharePoint Protection12](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection14.png)
4. Hello DPM에에서 표시 되는 hello SharePoint 개체 클릭 **복구** tooget hello 콘텐츠 데이터베이스 구조를 탭 합니다. Hello 항목을 마우스 오른쪽 단추로 누른 **복구**합니다.
   
    ![DPM SharePoint Protection13](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection15.png)
5. 이 시점에서 hello에 따라 [이 문서의 앞부분에서 복구 단계](#restore-a-sharepoint-item-from-disk-using-dpm) toorecover 디스크에서 SharePoint 콘텐츠 데이터베이스입니다.

## <a name="faqs"></a>FAQ
Q: SQL Server 2014 및 SQL 2012(SP2)를 지원하는 DPM 버전은 무엇인가요?<br>
A: DPM 2012 R2 업데이트 롤업 4 버전이 두 가지를 모두 지원합니다.

Q: 수 복구 SharePoint 항목 toohello 원래 위치 (디스크 보호)로 SQL AlwaysOn을 사용 하 여 SharePoint를 구성한 경우?<br>
A: 예, hello 항목 복구 된 toohello 원래 SharePoint 사이트 일 수 있습니다.

Q: 수 복구 SharePoint 데이터베이스 toohello 원래 위치로 SQL AlwaysOn을 사용 하 여 SharePoint를 구성한 경우?<br>
A: 하기 때문에 SharePoint 데이터베이스는 SQL AlwaysOn으로 구성 된 hello 가용성 그룹을 제거 하지 않으면 수정할 수 없습니다. 결과적으로, DPM 데이터베이스 toohello 원래 위치를 복원할 수 없습니다. SQL Server 데이터베이스 tooanother SQL Server 인스턴스를 복구할 수 있습니다.

## <a name="next-steps"></a>다음 단계
* SharePoint의 DPM 보호에 대한 자세한 정보는 [SharePoint의 DPM 보호를 위한 비디오 시리즈](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)
* [System Center 2012 - Data Protection Manager에 대한 릴리스 정보](https://technet.microsoft.com/library/jj860415.aspx)
* [System Center 2012 SP1의 Data Protection Manager에 대한 릴리스 정보](https://technet.microsoft.com/library/jj860394.aspx)

