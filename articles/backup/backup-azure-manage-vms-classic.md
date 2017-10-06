---
title: "Azure 가상 컴퓨터 백업을 aaaManage 및 모니터 | Microsoft Docs"
description: "어떻게 toomanage 모니터 Azure 가상 컴퓨터 및 백업에 알아봅니다"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 4372944e-d33a-4f6a-bd5f-d04af2842713
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: trinadhk;markgal;
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cb95e0b3760c96f7fd563c42cb4c635553f48957
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-common-azure-backup-jobs-and-trigger-alerts-in-hello-classic-portal"></a>일반적인 Azure 백업 작업 및 hello 클래식 포털에서 트리거 경고 관리
> [!div class="op_single_selector"]
> * [Azure VM 백업 관리](backup-azure-manage-vms.md)
> * [클래식 VM 백업 관리](backup-azure-manage-vms-classic.md)
>
>

이 문서에서는 Azure에서 보호되는 클랙식 모델 가상 컴퓨터에 대한 일반적인 관리 및 모니터링 관련 정보를 제공합니다.  

> [!NOTE]
> Azure에는 리소스를 만들고 작업하기 위한 두 가지 배포 모델인 [리소스 관리자와 클래식](../azure-resource-manager/resource-manager-deployment-model.md)모델이 있습니다. 참조 [Azure 가상 컴퓨터를 사용자 환경 tooback 준비](backup-azure-vms-prepare.md) 클래식 배포 작업에 대 한 자세한 내용은 Vm을 모델링 합니다.
>
> [!IMPORTANT]
>2017 년 3 월 부터는 hello 클래식 포털 toocreate 백업 자격 증명 모음은 더 이상 사용할 수 없습니다.
>
> 이제 사용자 백업 자격 증명 모음 tooRecovery 서비스 자격 증명 모음을 업그레이드할 수 있습니다. 자세한 내용은 hello 문서 참조 [복구 서비스 자격 증명 모음에 백업 자격 증명 모음 tooa 업그레이드](backup-azure-upgrade-backup-to-recovery-services.md)합니다. Microsoft는 것이 권장 tooupgrade 백업 tooRecovery 서비스 자격 증명 모음 자격 증명 모음입니다.<br/> 2017 년 10 월 15 후 PowerShell toocreate 백업 자격 증명 모음을 사용할 수 없습니다. **2017년 11월 1일까지**:
>- 모든 나머지 백업 자격 증명 모음을 자동으로 업그레이드 된 tooRecovery 서비스 자격 증명 모음 됩니다.
>- 하면 hello 클래식 포털에서 수 tooaccess 백업 데이터 수 없습니다. 대신, 복구 서비스 자격 증명 모음에 hello Azure 포털 tooaccess 백업 데이터를 사용 합니다.

## <a name="manage-protected-virtual-machines"></a>보호된 가상 컴퓨터 관리
toomanage 보호 되는 가상 컴퓨터:

1. tooview hello를 클릭 하는 가상 컴퓨터에 대 한 백업 설정을 관리 하 고 **보호 된 항목** 탭 합니다.
2. 보호 된 항목 toosee hello의 hello 이름을 클릭 **백업 세부 정보** hello 마지막 백업에 대 한 정보를 보여 주는 탭 합니다.

    ![가상 컴퓨터 백업](./media/backup-azure-manage-vms/backup-vmdetails.png)
3. tooview hello를 클릭 하는 가상 컴퓨터에 대 한 백업 정책 설정을 관리 하 고 **정책** 탭 합니다.

    ![가상 컴퓨터 정책](./media/backup-azure-manage-vms/manage-policy-settings.png)

    hello **백업 정책** 기존 정책을 hello 표시를 탭 합니다. 필요에 따라 수정할 수 있습니다. 새 정책 toocreate 필요 하면 클릭 **만들기** hello에 **정책** 페이지. Note 하 tooremove 하려는 경우 정책을 안는 연결 된 모든 가상 컴퓨터.

    ![가상 컴퓨터 정책](./media/backup-azure-manage-vms/backup-vmpolicy.png)
4. 가상 컴퓨터 hello에 대 한 작업 또는 상태에 대 한 자세한 정보를 얻을 수 **작업** 페이지. 자세한 내용은 또는 특정 가상 컴퓨터에 대 한 작업을 필터링 hello 목록 tooget에서 작업을 클릭 합니다.

    ![작업](./media/backup-azure-manage-vms/backup-job.png)

## <a name="on-demand-backup-of-a-virtual-machine"></a>가상 컴퓨터의 주문형 백업
보호를 위해 구성한 후에는 가상 컴퓨터의 주문형 백업을 수행할 수 있습니다. Hello 초기 백업을 보류 중인 경우 hello 가상 컴퓨터에 대 한 주문형 백업 복사본이 생성 됩니다. 전체 hello 가상 컴퓨터의 Azure 백업 자격 증명 모음에 있습니다. 첫 번째 백업이 완료 되 면 경우 주문형으로 백업 됩니다 송신 변경 내용을 이전 백업 tooAzure 백업에서 자격 증명 모음, 즉 것만 항상 증가 합니다.

> [!NOTE]
> 요청 시 백업의 보존 범위 백업 정책 해당 toohello VM 매일 보존 기간에 대해 지정 된 tooretention 값으로 설정 되어 있습니다.  
>
>

가상 컴퓨터의 주문형 tootake 백업:

1. Toohello 이동 **보호 된 항목** 페이지를 선택 **Azure 가상 컴퓨터** 으로 **형식** (아직 선택 되지 않은) 하는 경우 클릭 하 고 **선택**단추입니다.

    ![VM 유형](./media/backup-azure-manage-vms/vm-type.png)
2. Hello 가상 컴퓨터를 주문형 tootake 백업을 클릭할 선택 **지금 백업** hello hello 페이지 맨 아래에 단추입니다.

    ![지금 백업](./media/backup-azure-manage-vms/backup-now.png)

    이렇게 하면 선택한 hello 가상 컴퓨터에서 백업 작업이 만들어집니다. 이 작업을 통해 생성 되는 복구 지점의 보존 범위는 hello 가상 컴퓨터와 연결 된 hello 정책에 지정 된 것과 동일한 됩니다.

    ![백업 작업 만들기](./media/backup-azure-manage-vms/creating-job.png)

   > [!NOTE]
   > hello에 가상 컴퓨터에 가상 컴퓨터를 드릴 다운 연관 tooview hello 정책 **보호 된 항목** 페이지와 이동 toobackup 정책 탭 합니다.
   >
   >
3. Hello 작업을 만든 후 클릭 **작업 보기** hello 알림 toosee hello hello 작업 페이지에서 해당 작업 표시줄에서 단추입니다.

    ![백업 작업 생성됨](./media/backup-azure-manage-vms/created-job.png)
4. Hello 작업을 성공적으로 완료 한 후는 복구 지점이 생성 될 수 있는 toorestore hello 가상 컴퓨터. 이 또한 hello 복구 지점 열 값 1 씩에 **보호 된 항목** 페이지.

## <a name="stop-protecting-virtual-machines"></a>가상 컴퓨터 보호 중지
다음 옵션 hello로 toostop hello 나중에 백업이 가상 컴퓨터를 선택할 수 있습니다.

* Azure 백업 자격 증명 모음에 가상 컴퓨터와 연결된 백업 데이터 유지
* 가상 컴퓨터와 연결된 백업 데이터 삭제

가상 컴퓨터와 연결 된 tooretain 백업 데이터를 선택한 경우에 hello 백업 데이터 toorestore hello 가상 컴퓨터를 사용할 수 있습니다. 이러한 가상 컴퓨터의 가격 정보를 보려면 [여기](https://azure.microsoft.com/pricing/details/backup/)를 클릭하세요.

가상 컴퓨터에 대 한 tooStop 보호:

1. 너무 이동**보호 된 항목** 페이지로 돌아간 후 선택 **Azure 가상 컴퓨터** hello 필터 형식 (아직 선택 되지 않은) 하는 경우 클릭으로 **선택** 단추입니다.

    ![VM 유형](./media/backup-azure-manage-vms/vm-type.png)
2. Hello 가상 컴퓨터를 선택 하 고 클릭 **보호 중지** hello hello 페이지 맨 아래에 있습니다.

    ![보호 중지](./media/backup-azure-manage-vms/stop-protection.png)
3. 기본적으로 Azure 백업 삭제 되지 않습니다 hello 가상 컴퓨터와 연결 된 hello 백업 데이터.

    ![보호 중지 확인](./media/backup-azure-manage-vms/confirm-stop-protection.png)

    Toodelete 백업 데이터를 원하는 경우 hello 확인란을 선택 합니다.

    ![확인란](./media/backup-azure-manage-vms/checkbox.png)

    Hello 백업 중지 이유를 선택 하십시오. 선택 사항 이지만는 이유를 입력 및 데 도움이 되 hello 피드백에 Azure 백업 toowork hello 고객 시나리오 우선 순위를 지정 합니다.
4. 클릭 **전송** 단추 toosubmit hello **보호를 중지** 작업 합니다. 클릭 **작업 보기** toosee hello에 해당 하는 hello 작업이 **작업** 페이지.

    ![보호 중지](./media/backup-azure-manage-vms/stop-protect-success.png)

    선택 하지 않은 경우 **연결 된 백업 데이터 삭제** 중 옵션 **보호 중지** post 작업 완료, 그런 다음 마법사를 보호 상태가 너무 변경**보호가 중지**. hello 데이터 명시적으로 삭제 될 때까지 Azure 백업으로 유지 됩니다. Hello에 hello 가상 컴퓨터를 선택 하 여 항상 hello 데이터를 삭제할 수 있습니다 **보호 된 항목** 페이지를 클릭 하 고 **삭제**합니다.

    ![보호 중지됨](./media/backup-azure-manage-vms/protection-stopped-status.png)

    Hello를 선택한 경우 **연결 된 백업 데이터 삭제** 옵션, hello 가상 컴퓨터에 포함 되지 hello **보호 된 항목** 페이지.

## <a name="re-protect-virtual-machine"></a>가상 컴퓨터 다시 보호
Hello를 선택 하지 않은 경우 **백업 데이터를 연결 하는 삭제** 옵션을 **보호 중지**를 수행 하 여 hello 가상 컴퓨터를 다시 보호할 수를 hello 단계 비슷한 toobacking 가상 등록 컴퓨터입니다. 보호를이 가상 컴퓨터 보관 되는 백업 데이터 이전 toostop protection 고 복구 지점 이후에 생성 되 면 다시 보호 합니다.

다시 보호 한 후 hello 가상 컴퓨터의 보호 상태가 변경 됩니다 너무**Protected** 지점이 있는 경우 복구 이전 너무**보호 중지**합니다.

  ![다시 보호된 VM](./media/backup-azure-manage-vms/reprotected-status.png)

> [!NOTE]
> Hello 가상 컴퓨터를 다시 보호 된 가상 컴퓨터를 보호 처음 hello 정책 보다 다른 정책을 선택할 수 있습니다.
>
>

## <a name="unregister-virtual-machines"></a>가상 컴퓨터 등록 취소
하려는 경우 hello 백업 자격 증명 모음에서 tooremove hello 가상 컴퓨터:

1. Hello 클릭 **등록 취소** hello hello 페이지 맨 아래에 단추입니다.

    ![보호 사용 안 함](./media/backup-azure-manage-vms/unregister-button.png)

    알림 메시지는 hello 확인을 요청 하는 hello 화면 맨 아래에 표시 됩니다. 클릭 **예** toocontinue 합니다.

    ![보호 사용 안 함](./media/backup-azure-manage-vms/confirm-unregister.png)

## <a name="delete-backup-data"></a>백업 데이터 삭제
하거나 가상 컴퓨터와 연결 된 hello 백업 데이터를 삭제할 수 있습니다.

* 보호 중지 작업 중
* 가상 컴퓨터에서 보호 중지 작업이 완료된 후

hello에 있는 가상 컴퓨터에서 백업 데이터 toodelete *보호가 중지* 상태 게시 성공적으로 완료 한 **백업 중지** 작업:

1. Toohello 이동 **보호 된 항목** 페이지를 선택 **Azure 가상 컴퓨터** 으로 *형식* hello 클릭 **선택** 단추입니다.

    ![VM 유형](./media/backup-azure-manage-vms/vm-type.png)
2. Hello 가상 컴퓨터를 선택 합니다. hello 가상 컴퓨터에 포함 됩니다 **보호가 중지** 상태입니다.

    ![보호 중지됨](./media/backup-azure-manage-vms/protection-stopped-b.png)
3. Hello 클릭 **삭제** hello hello 페이지 맨 아래에 단추입니다.

    ![백업 삭제](./media/backup-azure-manage-vms/delete-backup.png)
4. Hello에 **백업 데이터를 삭제** 마법사 (권장 사항) 백업 데이터를 삭제 하기 위한 이유를 선택 하 고 클릭 **전송**합니다.

    ![백업 데이터 삭제](./media/backup-azure-manage-vms/delete-backup-data.png)
5. 그러면 선택한 가상 컴퓨터의 작업 toodelete 백업 데이터를 생성 됩니다. 클릭 **작업 보기** toosee 작업 페이지에서 해당 작업 합니다.

    ![데이터 삭제 성공](./media/backup-azure-manage-vms/delete-data-success.png)

    Hello 작업이 완료 되 면 해당 toohello 가상 컴퓨터에서 제거할 항목 hello **보호 된 항목** 페이지.

## <a name="dashboard"></a>대시보드
Hello에 **대시보드** 페이지 Azure 가상 컴퓨터, 저장소 및에 관련 된 hello 지난 24 시간 동안 작업에 대 한 정보를 검토할 수 있습니다. 백업 상태 및 연결된 백업 오류를 볼 수 있습니다.

![대시보드](./media/backup-azure-manage-vms/dashboard-protectedvms.png)

> [!NOTE]
> Hello 대시보드의 값은 24 시간 마다 새로 고쳐집니다.
>
>

## <a name="auditing-operations"></a>작업 감사
Azure 백업 "작업" 작업 로그를 백업 쉽게 toosee hello 백업 자격 증명 모음에 대해 어떤 관리 작업이 정확 하 게 만드는 hello 고객에 의해 트리거되 hello에 대 한 검토를 제공 합니다. 작업 로그 훌륭한 사후를 사용 하도록 설정 하 고 hello 백업 작업에 대 한 지원을 감사 합니다.

작업을 수행 하는 hello 작업 로그에 기록 됩니다.

* 등록
* 등록 취소
* 보호 구성
* 백업(예약된 백업 및 BackupNow 통해 요청된 백업 모두)
* 복원
* 보호 중지
* 백업 데이터 삭제
* 정책 추가
* 정책 삭제
* 정책 업데이트
* 작업 취소

tooview 작업이 해당 tooa 백업 자격 증명 모음을 기록합니다.

1. 너무 이동**관리 서비스** Azure 포털에서 다음 hello를 클릭 하 고 **작업 로그** 탭 합니다.

    ![작업 로그](./media/backup-azure-manage-vms/ops-logs.png)
2. Hello 필터 선택 **백업** 으로 *형식* hello 백업 자격 증명 모음 이름을 지정 하 고 *서비스 이름* 을 클릭할 **전송**합니다.

    ![작업 로그 필터](./media/backup-azure-manage-vms/ops-logs-filter.png)
3. Hello 작업 로그에서 모든 작업을 선택 하 고 클릭 **세부 정보** toosee 해당 tooan 작업에 자세히 설명 합니다.

    ![작업 로그 Fetching 세부 정보](./media/backup-azure-manage-vms/ops-logs-details.png)

    hello **세부 정보 마법사** hello 작업, 작업 Id, 된 리소스를이 작업을 트리거할 hello 작업의 시작 시간에 대 한 정보를 포함 합니다.

    ![작업 세부 정보](./media/backup-azure-manage-vms/ops-logs-details-window.png)

## <a name="alert-notifications"></a>경고 알림
Hello 작업에 대 한 사용자 지정 경고 알림을 포털에서 얻을 수 있습니다. 작업 로그 이벤트에서 PowerShell 기반 경고 규칙을 정의하여 수행됩니다. *PowerShell 버전 1.3.0 이상*을 사용하는 것이 좋습니다.

백업 실패에 대 한 사용자 지정 알림 tooalert toodefine 샘플 명령은 같이 표시 됩니다.

```
PS C:\> $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail contoso@microsoft.com
PS C:\> Add-AzureRmLogAlertRule -Name backupFailedAlert -Location "East US" -ResourceGroup RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US -OperationName Microsoft.Backup/backupVault/Backup -Status Failed -TargetResourceId /subscriptions/86eeac34-eth9a-4de3-84db-7a27d121967e/resourceGroups/RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US/providers/microsoft.backupbvtd2/BackupVault/trinadhVault -Actions $actionEmail
```

**ResourceId**: 이 섹션에서 설명한 것처럼 작업 로그 팝업에서 가져올 수 있습니다. ResourceUri 작업의 정보 팝업 창에서이 cmdlet에 제공 된 hello ResourceId toobe입니다.

**OperationName**: hello 형식의 됩니다 "Microsoft.Backup/backupvault/<EventName>" 여기서 EventName는 레지스터, 등록 취소, ConfigureProtection, 백업, 복원, StopProtection, DeleteBackupData, 중 하나 CreateProtectionPolicy, DeleteProtectionPolicy, UpdateProtectionPolicy

**상태**: 지원되는 값은 시작함, 성공함 및 실패함입니다.

**ResourceGroup**: 작업이 트리거되면 hello 리소스의 리소스 그룹입니다. ResourceId 값에서 얻을 수 있습니다. 값 필드 간의 */resourceGroups/* 및 */providers/* ResourceId 값은 리소스 그룹에 대 한 hello 값입니다.

**이름**: hello 경고 규칙의 이름입니다.

**CustomEmail**: hello 사용자 지정 전자 메일 주소 toowhich toosend 경고 알림을 지정

**SendToServiceOwners**:이 옵션 경고 알림 tooall 관리자와 hello 구독의 공동 관리자를 보냅니다. **New-AzureRmAlertRuleEmail** cmdlet에 사용될 수 있음

### <a name="limitations-on-alerts"></a>경고에 대한 제한
이벤트 기반 경고는 다음과 같은 제한을 거쳐야 toohello:

1. Hello 백업 자격 증명 모음에 있는 모든 가상 컴퓨터에 경고가 트리거됩니다. 사용자 지정할 수 것 백업 자격 증명 모음에 있는 가상 컴퓨터의 특정 집합에 대 한 tooget 경고 합니다.
2. 이 기능은 미리 보기 상태입니다. [자세히 알아보기](../monitoring-and-diagnostics/insights-powershell-samples.md#create-metric-alerts)
3. “alerts-noreply@mail.windowsazure.com”에서 경고를 받게 됩니다. 현재 hello 전자 메일 보낸 사람을 수정할 수 없습니다.

## <a name="next-steps"></a>다음 단계
* [Azure VM 복원](backup-azure-restore-vms.md)
