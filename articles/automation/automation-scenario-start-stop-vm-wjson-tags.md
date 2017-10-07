---
title: "JSON 형식 태그 tooschedule Azure VM 상태 aaaUse | Microsoft Docs"
description: "이 문서에서는 VM 시작 및 종료의 tooautomate hello 예약 태그 toouse JSON 문자열 하는 방법을 보여줍니다."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 6afed5d2-e939-4749-8b2c-9312b4c16fb2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: magoedte;paulomarquesc
ms.openlocfilehash: f6bbf1dea1c193e5d1010f12f3b1ed63562f9daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario-using-json-formatted-tags-toocreate-a-schedule-for-azure-vm-startup-and-shutdown"></a>Azure 자동화 시나리오: JSON 형식를 사용 하 여 Azure VM 시작 및 종료에 대 한 일정 toocreate 태그 지정
고객 tooschedule hello 시작은 경우가 종종 및 toohelp 가상 컴퓨터의 종료 구독 비용을 줄이거나 비즈니스 및 기술 요구 사항을 지원 합니다.

hello 다음과 같은 시나리오 사용 하면 tooset를 자동된 시작 및 종료 Vm의 리소스 그룹 수준 또는 Azure에서 가상 컴퓨터 수준에서 일정 라고 하는 태그를 사용 하 여 합니다. 시작 시간과 종료 시간 일요일 tooSaturday에서이 일정을 구성할 수 있습니다.

일부의 기본 옵션이 있습니다. 내용은 다음과 같습니다.

* [가상 컴퓨터 크기 집합](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) tooscale / 축소를 사용할 수 있는 자동 크기 조정 설정을 사용 하 여 합니다.
* [DevTest Labs](../devtest-lab/devtest-lab-overview.md) 서비스 기능이 hello 기본 제공 된 시작 및 종료 작업 일정입니다.

그러나 이러한 옵션 특정 시나리오를만 지원 하며 적용된 tooinfrastructure-as a service (IaaS) Vm 수는 없습니다.

적용 된 tooa 리소스 그룹 hello 태그 일정을 사용 하는 경우 해당 리소스 그룹 내의 가상 컴퓨터 적용 된 tooall 이기도 합니다. 일정에 따라 직접 적용 된 tooa VM 이면 hello 마지막 일정 우선 순서에 따라 hello에:

1. 일정 적용 된 tooa 리소스 그룹
2. 적용 된 tooa 리소스 그룹 및 hello 리소스 그룹에 가상 컴퓨터를 예약 합니다.
3. 적용 되는 일정 tooa 가상 컴퓨터

이 시나리오에서 기본적으로 지정 된 형식으로 JSON 문자열을 사용 하 고 hello 값으로 추가 Schedule 이라는 태그에 대 한 합니다. 다음 runbook는 모든 리소스 그룹 및 가상 컴퓨터를 나열 하 고 앞에서 나열 된 hello 시나리오에 따라 각 VM에 대 한 hello 일정을 식별 합니다. 다음 hello 첨부 된 일정이 있는 Vm 반복 하 고 평가 어떤 작업을 수행 해야 합니다. 예를 들어 Vm 중지 하거나 종료 하거나 무시 toobe 필요한 결정 합니다.

이러한 runbook hello를 사용 하 여 인증 [Azure 실행 계정](automation-sec-configure-azure-runas-account.md)합니다.

## <a name="download-hello-runbooks-for-hello-scenario"></a>Hello 시나리오에 대 한 hello runbook 다운로드
이 시나리오 hello에서 다운로드할 수 있는 4 개의 PowerShell 워크플로 runbook 이루어져 [TechNet 갤러리](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) 또는 hello [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) 이 프로젝트에 대 한 저장소입니다.

| Runbook | 설명 |
| --- | --- |
| Test-ResourceSchedule |각 가상 컴퓨터 일정을 확인 하 고 종료 또는 hello 일정에 따라 시작을 수행 합니다. |
| Add-ResourceSchedule |Hello는 일정 태그 tooa VM 또는 리소스 그룹을 추가합니다. |
| Update-ResourceSchedule |새 항목으로 대체 하 여 hello 기존 일정 태그를 수정 합니다. |
| Remove-ResourceSchedule |VM 또는 리소스 그룹에서 hello 일정 태그를 제거합니다. |

## <a name="install-and-configure-this-scenario"></a>이 시나리오 설치 및 구성
### <a name="install-and-publish-hello-runbooks"></a>설치 하 고 hello runbook 게시
Hello runbook에 다운로드 한 후에 가져올 수의 hello 절차를 사용 하 여 [만들기 또는 Azure 자동화에서 runbook을 가져와](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation)합니다.  각 Runbook을 자동화 계정으로 가져온 후에 게시합니다.

### <a name="add-a-schedule-toohello-test-resourceschedule-runbook"></a>일정 toohello ResourceSchedule 테스트 runbook을 추가
이러한 단계 tooenable hello hello 테스트 ResourceSchedule runbook에 대 한 일정에 따라 합니다. 가상 컴퓨터를 시작 해야 함, 종료, 확인 하는 hello runbook 또는 왼쪽 그대로입니다.

1. Hello Azure 포털에서에서 자동화 계정을 열고 hello 클릭 **Runbook** 바둑판식으로 배열입니다.
2. Hello에 **테스트 ResourceSchedule** 블레이드에서 hello 클릭 **일정** 바둑판식으로 배열입니다.
3. Hello에 **일정** 블레이드에서 클릭 **일정을 추가할**합니다.
4. Hello에 **일정** 블레이드를 **일정 tooyour runbook을 연결**합니다. 그런 다음 **새 일정 만들기**를 선택합니다.
5. Hello에 **새 일정** 블레이드에서 hello 이름에이 일정을 유형의 예를 들어: *HourlyExecution*합니다.
6. Hello 일정에 대 한 **시작**, hello 시작 시간 tooan 시간 증분을 설정 합니다.
7. **되풀이**를 선택한 다음 **되풀이 간격**에서 **1시간**을 선택합니다.
8. 되어 있는지 확인 **세트 만료** 너무 설정**아니요**, 클릭 하 고 **만들기** toosave 새 일정.
9. Hello에 **일정 Runbook** 옵션 블레이드에서 **매개 변수 및 실행된 설정**합니다. 테스트 ResourceSchedule hello에 **매개 변수** 블레이드에서 hello에 구독 hello 이름을 입력 **SubscriptionName** 필드입니다.  이 hello runbook에 대 한 필요한 hello 유일한 매개 변수입니다.  작업을 완료하면 **확인**을 클릭합니다.

완료 되 면 hello runbook 일정 hello 다음과 같이 표시 됩니다.

![구성된 Test-ResourceSchedule Runbook](./media/automation-scenario-start-stop-vm-wjson-tags/automation-schedule-config.png)<br>

## <a name="format-hello-json-string"></a>형식 hello JSON 문자열
기본적으로이 솔루션은 JSON으로 지정된 된 형식으로 문자열을 태그에 대 한 hello 값으로 추가 일정을 호출 합니다. 다음 runbook는 모든 리소스 그룹 및 가상 컴퓨터를 나열 하 고 각 가상 컴퓨터에 대 한 hello 일정을 식별 합니다.

hello runbook hello 가상 컴퓨터를 연결 하는 일정을 반복 하 고 어떤 조치를 확인 합니다. hello 다음은 hello 솔루션 포맷할 방법의 예입니다.

```json
{
    "TzId": "Eastern Standard Time",
    "0": {
        "S": "11",
        "E": "17"
    },
    "1": {
        "S": "9",
        "E": "19"
    },
    "2": {
        "S": "9",
        "E": "19"
    },
}
```

이 구조에 대한 자세한 정보 다음과 같습니다.

1. hello이 JSON 구조 형식이 최적화 toowork Azure에서 단일 태그 값의 hello 256 자 제한 해결 합니다.
2. *TzId* hello 가상 컴퓨터의 표준 시간대를 hello 나타냅니다. PowerShell 세션-의 hello TimeZoneInfo.NET 클래스를 사용 하 여이 ID를 가져올 수 있습니다**[System.TimeZoneInfo]:: GetSystemTimeZones()**합니다.

   ![PowerShell의 GetSystemTimeZones](./media/automation-scenario-start-stop-vm-wjson-tags/automation-get-timzone-powershell.png)

   * 평일 0 toosix의 숫자 값으로 표시 됩니다. hello 값 0은 일요일을 같습니다.
   * hello 시작 시간으로 표시 됩니다 hello **S** 특성과 해당 값은 24 시간 형식입니다.
   * hello 끝 또는 종료 시간 표현 됩니다 hello로 **E** 특성과 해당 값은 24 시간 형식입니다.

     경우 hello **S** 및 **E** 각 특성에는 영 (0)의 값은, 평가 hello 시 hello 가상 컴퓨터를 현재 상태에서 유지 됩니다.
3. Hello 주의 특정 요일에 대 한 tooskip 평가 하려는 경우 hello 주의 해당 요일에 대 한 섹션을 추가 하지 마십시오. Hello에 다음 예제에서는 월요일만 평가 되 고 hello hello 요일을 다른 무시 됩니다.

    ```json
    {
        "TzId": "Eastern Standard Time",
        "1": {
            "S": "11",
            "E": "17"
        }
    }
    ```

## <a name="tag-resource-groups-or-vms"></a>리소스 그룹 또는 VM 태그 지정
Vm 아래로 tooshut, 해야 tootag hello Vm 또는는 날짜별 hello 리소스 그룹 중 하나입니다. Schedule 태그가 없는 가상 컴퓨터는 평가되지 않습니다. 따라서 시작되거나 종료되지 않습니다.

이 솔루션에 두 가지 방법으로 tootag 리소스 그룹 또는 Vm 있습니다. Hello 포털에서 직접 작업할 수 있습니다. 또는 hello ResourceSchedule 추가, 업데이트-ResourceSchedule 및 제거 ResourceSchedule runbook을 사용할 수 있습니다.

### <a name="tag-through-hello-portal"></a>Hello 포털을 통해 태그
이러한 단계 tootag 가상 컴퓨터 또는 hello 포털에서 리소스 그룹을 수행 합니다.

1. Hello JSON 문자열을 결합 하 고 공백이 되지 해당 확인 합니다.  JSON 문자열은 다음과 같아야 합니다.

    ```json
    {"TzId":"Eastern Standard Time","0":{"S":"11","E":"17"},"1":{"S":"9","E":"19"},"2": {"S":"9","E":"19"},"3":{"S":"9","E":"19"},"4":{"S":"9","E":"19"},"5":{"S":"9","E":"19"},"6":{"S":"11","E":"17"}}
    ```

2. 선택 hello **태그** VM 또는 리소스에 대 한 아이콘 그룹 tooapply이이 일정을 설정 합니다.

   ![VM 태그 옵션](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-tag-option.png)

3. 태그는 다음 키/값 쌍으로 정의됩니다. 형식 **일정** hello에 **키** 필드를 선택한 다음 hello에 hello JSON 문자열을 붙여 **값** 필드입니다. **Save**를 클릭합니다. 이제 새 태그를 리소스에 대 한 태그의 hello 목록에 나타납니다.

   ![VM Schedule 태그](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-schedule-tag.png)

### <a name="tag-from-powershell"></a>PowerShell에서 태그 지정
가져온된 모든 runbook tooexecute PowerShell에서 직접 runbook hello 하는 방법을 설명 하는 hello 스크립트의 hello 시작 부분에 도움말 정보를 포함 합니다. PowerShell에서 hello ScheduleResource 추가 및 업데이트 ScheduleResource runbook을 호출할 수 있습니다. Hello 포털 외부에서 VM 또는 리소스 그룹에 toocreate 또는 업데이트 hello 일정 태그 수 있는 필수 매개 변수를 전달 하 여이 작업을 수행 합니다.

먼저 너무 toocreate, 추가 및 PowerShell 통해 태그를 삭제,[Azure에 대 한 PowerShell 환경을 설정](/powershell/azure/overview)합니다. Hello 설치를 완료 한 후 단계를 수행 하는 hello를 진행할 수 있습니다.

### <a name="create-a-schedule-tag-with-powershell"></a>PowerShell을 사용하여 Schedule 태그 만들기
1. PowerShell 세션을 엽니다. 다음 예제에서는 tooauthenticate 실행 계정 및 구독 toospecify hello를 사용 하 여.

    ```powershell
    $Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. 일정 해시 테이블을 정의합니다. 다음은 생성 방법의 예입니다.

    ```powershell
    $schedule= @{ "TzId"="Eastern Standard Time"; "0"= @{"S"="11";"E"="17"};"1"= @{"S"="9";"E"="19"};"2"= @{"S"="9";"E"="19"};"3"= @{"S"="9";"E"="19"};"4"= @{"S"="9";"E"="19"};"5"= @{"S"="9";"E"="19"};"6"= @{"S"="11";"E"="17"}}
    ```

3. Hello runbook에 필요한 hello 매개 변수를 정의 합니다. 다음 예제는 hello, VM 대상:

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "VmName"="VM01";"Schedule"=$schedule}
    ```

    리소스 그룹을 태그 지정 하는 경우 제거 hello *VMName* hello $params 해시에서 매개 변수는 다음과 같이 테이블:

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "Schedule"=$schedule}
    ```

4. 매개 변수 toocreate hello 일정 태그 뒤 hello로 추가 ResourceSchedule hello runbook을 실행 합니다.

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Add-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

5. 리소스 그룹 또는 가상 컴퓨터 태그 tooupdate 실행 hello **업데이트 ResourceSchedule** runbook 매개 변수 뒤 hello로:

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Update-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

### <a name="remove-a-schedule-tag-with-powershell"></a>PowerShell을 사용하여 Schedule 태그 삭제
1. PowerShell 세션을 열고 하 고 다음 실행 계정 및 tooselect tooauthenticate hello를 실행 한 구독을 지정:

    ```powershell
    Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. Hello runbook에 필요한 hello 매개 변수를 정의 합니다. 다음 예제는 hello, VM 대상:

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01";"VmName"="VM01"}
    ```

    리소스 그룹에서 태그를 제거 하는 경우 제거 hello *VMName* hello $params 해시에서 매개 변수는 다음과 같이 테이블:

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"}
    ```

3. Hello 제거 ResourceSchedule runbook tooremove hello 일정 태그를 실행 합니다.

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

4. tooupdate 리소스 그룹 또는 가상 컴퓨터 태그를 매개 변수 뒤 hello로 hello 제거 ResourceSchedule runbook을 실행 합니다.

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

> [!NOTE]
> 사전를 모니터링 되는 가상 컴퓨터 tooverify 종료 이러한 runbook (및 hello 가상 컴퓨터 상태)을 권장 하 고 적절 하 게 시작 합니다.
>

hello 테스트 ResourceSchedule runbook의 tooview hello 세부 정보 선택 hello Azure 포털에서 hello 작업 **작업** hello runbook의 타일입니다. hello 작업 요약 표시 hello 입력된 매개 변수 및 hello 출력 스트림, 또한 hello 작업에 대 한 toogeneral 정보 및 예외 발생 한 경우.

hello **작업 요약** hello 출력, 경고 및 오류 스트림에서 메시지가 포함 됩니다. 선택 hello **출력** tooview 타일 hello runbook 실행의 결과 자세히 설명 합니다.

![Test-ResourceSchedule 출력](./media/automation-scenario-start-stop-vm-wjson-tags/automation-job-output.png)

## <a name="next-steps"></a>다음 단계
* PowerShell 워크플로 runbook 시작 tooget 참조 [내 첫 번째 PowerShell 워크플로 runbook](automation-first-runbook-textual.md)합니다.
* runbook 형식이 장점 및 제한 사항에 대해 자세히 toolearn 참조 [Azure 자동화 runbook 형식](automation-runbook-types.md)합니다.
* PowerShell 스크립트 지원 기능에 대한 자세한 내용은 [Azure 자동화에서 네이티브 PowerShell 스크립트 지원](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)을 참조하세요.
* runbook 로깅이 및 출력에 대해 자세히 toolearn 참조 [Runbook 출력 및 메시지 Azure 자동화에서](automation-runbook-output-and-messages.md)합니다.
* Azure 실행 계정 및 tooauthenticate runbook을 사용 하 여 확인 하려면 어떻게 해야 하는 방법에 대 한 자세한 toolearn [Azure 실행 계정 사용 하 여 runbook을 인증](automation-sec-configure-azure-runas-account.md)합니다.
