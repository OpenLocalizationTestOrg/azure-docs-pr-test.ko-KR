---
title: "aaaManage Azure 복구 서비스 자격 증명 모음 및 서버 | Microsoft Docs"
description: "이 자습서 toolearn toomanage Azure 복구 서비스 자격 증명 모음 및 서버를 사용 합니다."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: 4eea984b-7ed6-4600-ac60-99d2e9cb6d8a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markgal
ms.openlocfilehash: b4c35c86faa0828b3c63a13b85c095c0cbaba50e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-recovery-services-vaults-and-servers-for-windows-machines"></a>Windows 컴퓨터용 Azure 복구 서비스 자격 증명 모음 및 서버 모니터링 및 관리
> [!div class="op_single_selector"]
> * [리소스 관리자](backup-azure-manage-windows-server.md)
> * [클래식](backup-azure-manage-windows-server-classic.md)
>
>

이 문서에서 hello Azure 포털 및 hello Microsoft Azure 백업 에이전트를 통해 사용할 수 있는 모니터 및 관리 작업이 백업 hello의 개요를 찾을 수 있습니다. 이 문서에서는 이미 Azure 구독이 있으며 하나 이상의 Recovery Services Vault 를 만들었다고 가정합니다.

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]


## <a name="open-a-recovery-services-vault"></a>Recovery Services Vault 열기

hello 복구 서비스 자격 증명 모음 대시보드 hello 세부 정보 또는 특성 복구 서비스 자격 증명 모음을 보여 줍니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com/) Azure 구독을 사용 하 여 합니다.
2. Hello 허브 메뉴에서 클릭 **더 서비스**합니다.

    ![Recovery Services Vault 목록 열기 1단계](./media/backup-azure-manage-windows-server/open-rs-vault-list.png) <br/>

3. 복구 서비스 자격 증명 모음 tooopen 사용 하는 것이 좋습니다. Hello 대화 상자에서 입력을 시작 **복구 서비스**합니다. Hello 목록이 필터링 됩니다 입력을 시작 하면 사용자의 입력에 기반 합니다. 클릭 **복구 서비스 자격 증명 모음** toodisplay hello 목록이 복구 서비스 구독에 자격 증명 모음입니다.

    ![복구 서비스 자격 증명 모음 만들기 1단계](./media/backup-azure-manage-windows-server/browse-to-rs-vaults-2.png) <br/>

    복구 서비스 자격 증명 모음 hello 목록이 열립니다.

    ![복구 서비스 자격 증명 모음 만들기 1단계](./media/backup-azure-manage-windows-server/list-of-rs-vaults.png) <br/>

4. 자격 증명 모음 hello 목록에서 hello hello tooopen 원하는 복구 서비스 자격 증명 모음 이름을 선택 합니다. hello 복구 서비스 자격 증명 모음 대시보드 블레이드를 엽니다.

    ![복구 서비스 자격 증명 모음 대시보드](./media/backup-azure-manage-windows-server/rs-vault-blade.png) <br/>

    Hello 복구 서비스 자격 증명 모음을 연 했으므로 hello 모니터링 또는 관리 작업 중 하나를 수행 합니다.

## <a name="monitor-backup-jobs-and-alerts"></a>백업 작업 및 경고 모니터링

작업을 모니터링 및 경고 hello에서 복구 서비스 자격 증명 모음 대시보드를 볼 위치:

* 백업 경고 세부 정보
* 파일 및 폴더 뿐 아니라 hello 클라우드에서 보호 되는 Azure 가상 컴퓨터
* Azure에서 사용되는 총 저장소
* 백업 작업 상태

![백업 대시보드 작업](./media/backup-azure-manage-windows-server/dashboard-tiles.png)

각이 타일에 hello 정보를 클릭 하면 관련된 작업을 관리 하는 hello 관련된 블레이드를 열립니다.

Hello 맨 hello 대시보드

* 사용할 수 있는 백업 작업에 대한 액세스를 제공하는 설정입니다.
* 자격 증명 모음에 백업-toohello 복구 서비스 새 파일 및 폴더 (또는 Azure Vm)를 백업 하는 데 도움이 됩니다.
* Delete-복구 서비스 자격 증명 모음 더 이상 사용 되지, toofree 저장 공간을 삭제할 수 없습니다. 삭제는 모든 보호 된 서버 hello 자격 증명 모음에서 삭제 한 후에 활성화 됩니다.

![백업 대시보드 작업](./media/backup-azure-manage-windows-server/dashboard-tasks.png)

## <a name="alerts-for-backups-using-azure-backup-agent"></a>Azure 백업 에이전트에 의한 백업 경고
| 경고 수준 | 전송되는 경고 |
| --- | --- |
| 중요 |백업 실패, 복구 실패 |
| Warning |(1 백 미만의 파일 toocorruption 문제 인해 백업 되지 않습니다 및 1 백만 개 이상의 파일이 성공적으로 백업) 경우 경고와 함께 완료 된 백업 |
| 정보 제공 |없음 |

## <a name="manage-backup-alerts"></a>백업 경고 관리
Hello 클릭 **백업 경고** 타일 tooopen hello **백업 경고** 블레이드 경고 및 관리 합니다.

![백업 경고](./media/backup-azure-manage-windows-server/manage-backup-alerts.png)

타일에 표시 하는 hello 백업 경고 수가 hello:

* 지난 24 시간 동안 확인되지 않은 중요한 경고
* 지난 24 시간 동안 확인되지 않은 경고

클릭는 각이 링크에서 이동할 toohello **백업 경고** 블레이드 (위험 또는 경고) 이러한 경고에 대 한 필터링 된 보기를 합니다.

Hello 백업 경고 블레이드에서 있습니다.

* 경고와 적절 한 정보 tooinclude hello를 선택 합니다.

    ![열 선택](./media/backup-azure-manage-windows-server/choose-alerts-colunms.png)
* 심각도, 상태 및 시작/종료 시간에 대한 경고를 필터링합니다.

    ![경고 필터링](./media/backup-azure-manage-windows-server/filter-alerts.png)
* 심각도, 빈도 및 받는 사람에 대한 알림을 구성하며 경고를 켜거나 끕니다.

    ![경고 필터링](./media/backup-azure-manage-windows-server/configure-notifications.png)

경우 **당 경고** 를 hello로 선택 **알림** 그룹화 또는 발생 하지 않습니다 전자 메일에 감소 하는 빈도입니다. 모든 경고에 대해 알림 1개가 발생합니다. Hello 기본 설정 이며 hello 확인 전자 메일 즉시 전송도 됩니다.

경우 **시간별 다이제스트** 를 hello로 선택 **알림** 하나의 전자 메일에는 인하 toohello 사용자 보내집니다 주파수 지난 1 시간 동안 hello에 생성 된 새 경고를 확인할 수 없습니다. 확인 전자 메일 hello 시간 hello 끝에 보내집니다.

심각도 수준에 따라 hello에 대 한 경고를 보낼 수 있습니다.

* 중요
* Warning
* 정보

Hello로 hello 경고를 비활성화 **비활성화** hello 작업 세부 정보 블레이드에서 단추입니다. 비활성화를 클릭하면 확인 참고 사항을 제공할 수 있습니다.

Hello 열을 선택 하면 tooappear hello로 hello 경고의 일환으로 원하는 **열 선택** 단추입니다.

> [!NOTE]
> Hello에서 **설정** 블레이드를 선택 하 여 백업 경고를 관리 **모니터링 및 보고서 > 경고 및 이벤트 > 백업 경고** 클릭 한 다음 **필터** 또는  **알림을 구성**합니다.
>
>

## <a name="manage-backup-items"></a>백업 항목 관리
이제 온-프레미스 백업 관리 hello 관리 포털에서 제공 됩니다. Hello 대시보드의 hello 백업 섹션에서는 hello **백업 항목** 타일 hello 백업 항목 수가 보호 toohello 자격 증명 모음을 표시 합니다.

클릭 **파일 폴더** hello 백업 항목 타일에 있습니다.

![백업 항목 타일](./media/backup-azure-manage-windows-server/backup-items-tile.png)

각각의 특정 백업 나열 된 항목 표시 집합 tooFile 폴더를 필터링 하는 hello 백업 항목 hello로 블레이드를 엽니다.

![백업 항목](./media/backup-azure-manage-windows-server/backup-item-list.png)

Hello 목록에서 특정 백업 항목을 선택 하는 경우 해당 항목에 대 한 hello 필수 세부 정보 표시 됩니다.

> [!NOTE]
> Hello에서 **설정** 블레이드를 선택 하 여 파일 및 폴더 관리 **보호 된 항목 > 백업 항목** 다음를 선택 하 고 **파일 폴더** hello에서 드롭다운 메뉴.
>
>

![설정에서 항목 백업](./media/backup-azure-manage-windows-server/backup-files-and-folders.png)

## <a name="manage-backup-jobs"></a>백업 작업 관리
온-프레미스 (hello 온-프레미스 서버는 tooAzure 백업) 하는 경우와 Azure 백업에 대 한 백업 작업 hello 대시보드에 표시 됩니다.

Hello hello 대시보드의 백업 섹션, hello 백업 작업 타일 hello 작업 수를 표시:

* 진행 중
* 지난 24 시간 동안 hello에 실패 했습니다.

toomanage 백업 작업을 클릭 하 여 hello **백업 작업** 타일을 hello 백업 작업 블레이드에서 열립니다.

![설정에서 항목 백업](./media/backup-azure-manage-windows-server/backup-jobs.png)

Hello 백업 작업 블레이드에서 hello로 사용할 수 있는 hello 정보를 수정 하면 **열 선택** hello hello 페이지 위쪽에 단추입니다.

사용 하 여 hello **필터** Azure 가상 컴퓨터 백업 파일 및 폴더 간에 단추 tooselect 합니다.

백업 된 파일 및 폴더를 표시 되지 않으면, 클릭 **필터** hello 페이지를 선택 hello 위쪽에 단추 **파일 및 폴더** hello 항목 유형 메뉴에서 합니다.

> [!NOTE]
> Hello에서 **설정** 블레이드를 선택 하 여 백업 작업을 관리 **모니터링 및 보고서 > 작업 > 백업 작업** 다음를 선택 하 고 **파일 폴더** hello 드롭다운에서 드롭다운 메뉴.
>
>

## <a name="monitor-backup-usage"></a>백업 사용 모니터링
Hello hello 대시보드의 백업 섹션, hello 백업 사용량 타일 Azure에서 사용 되는 hello 저장소를 표시 합니다. 다음에 대한 저장소 사용량이 제공됩니다.

* Hello 자격 증명 모음과 연결 된 클라우드 LRS 저장소 사용량
* Hello 자격 증명 모음과 연결 된 클라우드 GRS 저장소 사용량

## <a name="manage-your-production-servers"></a>프로덕션 서버 관리
toomanage 프로덕션 서버를 클릭 하 여 **설정을**합니다.

관리 아래에서 **백업 인프라 > 프로덕션 서버**를 클릭합니다.

모든 사용 가능한 환경 서버 hello 프로덕션 서버 블레이드 나열 합니다. 서버 hello 목록 tooopen hello 서버 세부 정보를 클릭 합니다.

![보호된 항목](./media/backup-azure-manage-windows-server/production-server-list.png)


## <a name="open-hello-azure-backup-agent"></a>열기 hello Azure 백업 에이전트
열기 hello **Microsoft Azure 백업 에이전트** (에 대 한 컴퓨터를 검색 하 여 찾을 *Microsoft Azure 백업*).

![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/snap-in-search.png)

Hello에서 **동작** hello hello 백업 에이전트가 있는 경우 콘솔의 오른쪽에 사용할 수 있는 수행한 관리 작업을 수행 하는 hello:

* 서버 등록
* 백업 예약
* 지금 백업
* 속성 변경

![Microsoft Azure 백업 에이전트 콘솔 작업](./media/backup-azure-manage-windows-server/console-actions.png)

> [!NOTE]
> 너무**데이터 복구**, 참조 [파일 tooa Windows server 또는 Windows 클라이언트 컴퓨터 복원](backup-azure-restore-windows-server.md)합니다.
>
>

## <a name="modify-hello-backup-schedule"></a>Hello 백업 일정 수정
1. Hello Microsoft Azure 백업 에이전트에서 클릭 **백업 예약**합니다.

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/schedule-backup.png)
2. Hello에 **백업 예약 마법사** hello 둡니다 **toobackup 항목 또는 시간 변경** 옵션을 선택 하 고 클릭 **다음**합니다.

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
3. Tooadd 원하는 하거나 hello에 항목을 변경 하면 **항목 선택 tooBackup** 화면 클릭 **항목 추가**합니다.

    설정할 수도 있습니다 **제외 설정** hello 마법사의이 페이지에서. Tooexclude 파일 또는 파일 형식을 추가 하기 위한 hello 프로시저를 읽을 경우 [제외 설정](#manage-exclusion-settings)합니다.
4. Hello 파일 및 폴더를 누르고 tooback를 원하는 선택 **알겠습니다**합니다.

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/add-items-modify.png)
5. Hello 지정 **백업 일정** 클릭 **다음**합니다.

    매일(하루에 최대 3회) 또는 매주 백업을 예약할 수 있습니다.

    ![Windows Server 백업에 대한 항목](./media/backup-azure-manage-windows-server/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > Hello 백업 일정은이에 자세히 설명 되어 지정 [문서](backup-azure-backup-cloud-as-tape.md)합니다.
   >

6. 선택 hello **보존 정책** hello 백업 복사본 및 클릭에 대 한 **다음**합니다.

    ![Windows Server 백업에 대한 항목](./media/backup-azure-manage-windows-server/select-retention-policy-modify.png)
7. Hello에 **확인** 화면 hello 정보를 검토 하 고 클릭 **마침**합니다.
8. Hello 마법사 hello 만들기가 완료 되 면 **백업 일정**, 클릭 **닫기**합니다.

    보호를 수정한 후 확인할 수 있습니다 toohello 이동 하 여 백업을 올바르게 트리거될 **작업** 백업 작업을 탭 하 고 hello에 변경 내용이 반영 되었는지 확인 합니다.

## <a name="enable-network-throttling"></a>네트워크 제한 사용

hello Azure 백업 에이전트 데이터 전송 시 네트워크 대역폭을 어떻게 사용 되는지 toocontrol 수 있는 조정 탭을 제공 합니다. 이 컨트롤 근무 시간 동안 데이터를 tooback 필요 하지만 다른 인터넷 트래픽과 hello 백업 프로세스 toointerfere 하지 않을 경우에 유용 합니다. 데이터의 제한 전송 tooback를 적용 하 고 활동을 복원 합니다.  

tooenable 제한:

1. Hello에 **백업 에이전트**, 클릭 **속성 변경**합니다.
2. Hello에 * * 조정 탭을 선택 **백업 작업에 대 한 인터넷 대역폭 제한을 사용 하도록 설정**합니다.

    ![네트워크 제한](./media/backup-azure-manage-windows-server/throttling-dialog.png)

    제한을 사용 하도록 설정 하는 동안 백업 데이터 전송에 대 한 대역폭을 허용 하는 hello 지정 **근무 시간** 및 **휴무 시간**합니다.

    hello 대역폭 값 512kbps (초당) 크기는 512kb부터 시작 하 고 too1023 m b / 초 (Mbps)을 이동할 수 있습니다. Hello 시작을 지정 하 고 완료를 수도 있습니다 **근무 시간**, hello 요일을 어떤 작업 것으로 간주 됩니다 (일)입니다. 근무 시간을 지정 하는 hello 외부 hello 시간은 간주 toobe 비 작업 시간입니다.
3. **확인**을 클릭합니다.

## <a name="manage-exclusion-settings"></a>제외 설정 관리
1. 열기 hello **Microsoft Azure 백업 에이전트** (에 대 한 컴퓨터를 검색 하 여 찾을 수 있습니다 *Microsoft Azure 백업*).

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/snap-in-search.png)
2. Hello Microsoft Azure 백업 에이전트에서 클릭 **백업 예약**합니다.

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/schedule-backup.png)
3. 백업 예약 마법사 hello hello를 그대로 둡니다 **toobackup 항목 또는 시간 변경** 옵션을 선택 하 고 클릭 **다음**합니다.

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
4. **제외 설정**을 클릭합니다.

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/exclusion-settings.png)
5. **제외 추가**를 클릭합니다.

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/add-exclusion.png)
6. Hello 위치를 선택 하 고 클릭 **확인**합니다.

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/exclusion-location.png)
7. Hello에 hello 파일 확장명 추가 **파일 형식을** 필드입니다.

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/exclude-file-type.png)

    .mp3 확장명 추가

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/exclude-mp3.png)

    tooadd 다른 확장 클릭 **제외 추가** 하 고 다른 파일 형식 확장명 (.jpeg 확장명을 추가 합니다.)을 입력 합니다.

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/exclude-jpg.png)
8. 모든 hello 확장을 추가 했으므로 클릭 **확인**합니다.
9. 클릭 하 여 hello 백업 예약 마법사를 통해 계속 **다음** hello까지 **확인 페이지**, 클릭 **마침**합니다.

    ![Windows Server 백업 예약](./media/backup-azure-manage-windows-server/finish-exclusions.png)

## <a name="frequently-asked-questions"></a>질문과 대답
**Q 1입니다. hello 백업 작업 상태 이유 하지 않는 것 가져오기에 즉시 반영 포털 hello Azure 백업 에이전트에서에서 완료 된 것으로 표시?**

A1. 없는 최대 지연 시간을 15 분 hello 백업 작업 상태 사이에 반영 됩니다 hello Azure 백업 에이전트 및 hello Azure 포털.

**백업 작업이 실패할 때 Q.2, 얼마나 오래 걸립니까 tooraise 경고?**

A. 2가 경고는 hello Azure 백업 실패의 20 분 내에서 발생 합니다.

**Q3. 알림이 구성된 경우 메일이 전송되지 않는 경우가 있나요?**

A3. 다음 경우 hello hello 알림 순서 tooreduce hello 경고 노이즈에 전송 되지 것입니다.

* 알림이 1 시간 마다 구성 및 경고가 발생 되 고 hello 시간 내에서 확인 하는 경우
* 작업이 취소됩니다.
* 원래 백업 작업이 진행 중이므로 두 번째 백업 작업이 실패했습니다.

## <a name="troubleshooting-monitoring-issues"></a>모니터링 문제 해결
**문제:** 작업 및/또는 hello Azure 백업 에이전트에서 경고 hello 포털에 표시 되지 않습니다.

**문제 해결 단계:** 프로세스 hello ```OBRecoveryServicesManagementAgent```, 보냅니다 hello 작업 및 경고 데이터 toohello Azure 백업 서비스입니다. 때때로 이 프로세스가 멈추거나 종료될 수 있습니다.

1. tooverify hello 프로세스가 실행 되지 않는, 열기 **작업 관리자** 하 고 있는지 확인 합니다. hello ```OBRecoveryServicesManagementAgent``` 프로세스가 실행 되 고 있습니다.
2. Hello 프로세스를 실행 하지 않는 이라고 가정할 엽니다 **제어판** hello 서비스 목록을 찾습니다. **Microsoft Azure Recovery Services 관리 에이전트**를 시작하거나 다시 시작합니다.

    자세한 내용은 hello 로그, 위치를 찾습니다.<br/>
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` 예:<br/>
   `C:\Program Files\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider0.errlog`

## <a name="next-steps"></a>다음 단계
* [Azure에서 Windows Server 또는 Windows 클라이언트 복원](backup-azure-restore-windows-server.md)
* Azure 백업에 대해 자세히 toolearn 참조 [Azure 백업 개요](backup-introduction-to-azure-backup.md)
* Hello 방문 [Azure 백업 포럼](http://go.microsoft.com/fwlink/p/?LinkId=290933)
