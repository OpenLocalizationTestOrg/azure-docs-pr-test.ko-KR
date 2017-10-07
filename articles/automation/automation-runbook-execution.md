---
title: "Azure 자동화에서 aaaRunbook 실행 | Microsoft Docs"
description: "Azure 자동화에서 runbook은 처리 하는 방법에 대 한 hello 세부 정보를 설명 합니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d10c8ce2-2c0b-4ea7-ba3c-d20e09b2c9ca
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/17/2017
ms.author: bwren
ms.openlocfilehash: bdb535675443353d44640bc7773de3f9dac5e42c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-execution-in-azure-automation"></a>Azure 자동화에서 Runbook 실행
Azure 자동화에서 Runbook을 시작하면 작업이 생성됩니다. 작업은 Runbook의 단일 실행 인스턴스입니다. Azure 자동화 작업 자가 toorun 각 작업을 할당 합니다. 작업자는 여러 Azure 계정에서 공유하지만 여러 자동화 계정의 작업은 서로 격리됩니다. 작업에 대 한 어떤 작업자 서비스 hello 요청에 대 한 제어가 없는 합니다.  단일 Runbook에서 동시에 여러 작업을 실행할 수 있습니다. Hello Azure 포털에서에서 runbook의 목록과 hello를 볼 때 각 runbook에 대해 시작 된 모든 작업의 hello 상태를 나열 합니다. 각 주문 tootrack hello 상태에서 각 runbook에 대 한 작업 목록이 hello를 볼 수 있습니다. Hello 다른 작업 상태에 대 한 참조 [작업 상태](#job-statuses)합니다.

hello 다음 그림에 대 한 runbook 작업의 수명 주기 hello [그래픽 runbook](automation-runbook-types.md#graphical-runbooks) 및 [PowerShell 워크플로 runbook](automation-runbook-types.md#powershell-workflow-runbooks)합니다.

![작업 상태 - PowerShell 워크플로](./media/automation-runbook-execution/job-statuses.png)

hello 다음 그림에 대 한 runbook 작업의 수명 주기 hello [PowerShell runbook](automation-runbook-types.md#powershell-runbooks)합니다.

![작업 상태 - PowerShell 스크립트](./media/automation-runbook-execution/job-statuses-script.png)

사용자 작업에 대 한 액세스 tooyour Azure는 연결 tooyour Azure 구독을 만들어서 리소스입니다. 만 해당 리소스 hello 공용 클라우드에서 액세스할 수 있는 경우 데이터 센터에서 액세스 tooresources를 권한이 있습니다.

## <a name="job-statuses"></a>작업 상태
hello 다음 표에 작업에 사용할 수 있는 여러 상태를 hello 있습니다.

| 가동 상태 | 설명 |
|:--- |:--- |
| Completed |hello 작업이 완료 되었습니다. |
| 실패 |에 대 한 [그래픽 및 PowerShell 워크플로 runbook](automation-runbook-types.md), toocompile hello runbook이 실패 했습니다.  에 대 한 [PowerShell 스크립트 runbook](automation-runbook-types.md), hello runbook이 실패 했습니다 toostart 또는 hello 작업에서 예외가 발생 합니다. |
| Failed, waiting for resources |hello에 도달 했으므로 hello 작업이 실패 했습니다 [공평 분배](#fairshare) 제한에 3 번 및에서 시작 된 hello 같은 검사점 또는 hello에서 hello runbook의 때마다 시작 합니다. |
| Queued |hello 작업에서 대기 리소스에 대 한 사용 가능한 자동화 작업자 toocome에서 시작할 수 있도록 합니다. |
| 시작 중 |hello 작업이 tooa 작업자에 할당 하 고 hello 시스템은 hello 프로세스를 시작 함입니다. |
| Resuming |hello 시스템이 일시 중단 된 hello 작업을 다시 시작의 hello 프로세스입니다. |
| 실행 중 |hello 작업이 실행 되 고 있습니다. |
| Running, waiting for resources |hello 작업 언로드된 hello에 도달 했으므로 [공평 분배](#fairshare) 제한 합니다. 잠시 후 마지막 검사점에서 작업이 다시 시작됩니다. |
| 중지됨 |hello 작업이 완료 되기 전에 hello 사용자가 중지 되었습니다. |
| 중지 중 |hello 시스템이 hello 작업을 중지의 hello 프로세스입니다. |
| 일시 중단 |hello 작업이 hello 사용자, hello 시스템 또는 hello runbook의 명령에 의해 일시 중단 되었습니다. 일시 중단 된 작업 다시 시작할 수 있으며, 마지막 검사점에서 또는 검사점에 없는 경우 hello hello runbook의 시작에서 다시 시작 합니다. 예외가 발생 하는 경우에 hello runbook hello 시스템에 의해 중단 됩니다. ErrorActionPreference 너무 설정 기본적으로**계속**, 의미 있는 오류 hello 작업이 계속 실행 합니다. 이 기본 설정 변수 너무 설정 되어 있으면**중지**, 오류 발생 시 hello 작업을 일시 중단 합니다.  너무 적용[그래픽 및 PowerShell 워크플로 runbook](automation-runbook-types.md) 만 합니다. |
| Suspending |hello 시스템 hello 사용자의 hello 요청에서 toosuspend hello 작업을 하려고 합니다. 일시 중단할 수 전에 hello runbook 다음 검사점을 도달 해야만 합니다. 이미 마지막 검사점을 지난 경우 완료되어야만 일시 중단할 수 있습니다.  너무 적용[그래픽 및 PowerShell 워크플로 runbook](automation-runbook-types.md) 만 합니다. |

## <a name="viewing-job-status-from-hello-azure-portal"></a>Hello Azure 포털에서에서 작업 상태 보기
모든 runbook 작업의 요약 된 상태를 보거나 hello Azure 포털 또는 Microsoft Operations Management Suite (OMS) 로그 분석 작업 영역 tooforward runbook 작업 상태와의 통합 구성 하 여 특정 runbook 작업의 세부 정보로 드릴 수 있습니다 및 작업 스트림 합니다.  OMS 로그 분석에 통합 하는 방법에 대 한 자세한 내용은 참조 [자동화 tooLog 분석 (OMS)에서 작업 상태 및 작업 스트림 전달](automation-manage-send-joblogs-log-analytics.md)합니다.  

### <a name="automation-runbook-jobs-summary"></a>Automation runbook 작업 요약
선택한 자동화 계정의 오른쪽 hello에 모든 아래에서 선택한 자동화 계정에 대 한 hello runbook 작업의 요약을 볼 수 **작업 통계** 바둑판식으로 배열입니다.<br><br> ![작업 통계 타일](./media/automation-runbook-execution/automation-account-job-status-summary.png).<br> 이 타일에는 개수 및 실행 된 모든 작업에 대 한 hello 작업 상태를 그래픽으로 표시 됩니다.  

Hello 타일을 누르면 hello **작업** 블레이드를 실행 하는 모든 작업의, 시작 및 완료 시간, 상태 및 작업 실행와 요약 된 목록이 포함 됩니다.<br><br> ![Automation 계정 작업 블레이드](./media/automation-runbook-execution/automation-account-jobs-status-blade.png)<br><br>  선택 하 여 작업의 hello 목록을 필터링 할 수 있습니다 **작업을 필터링** 및 작업 상태, 특정 runbook을 필터링 또는 hello 드롭 다운 목록에서 날짜/시간 범위 toosearch 내을 환영 합니다.<br><br> ![작업 상태 필터링](./media/automation-runbook-execution/automation-account-jobs-filter.png)

또는 hello에서 해당 runbook을 선택 하 여 작업이 특정 runbook에 대 한 요약 정보를 볼 수 있습니다 **Runbook** 자동화 계정 및 선택 hello 블레이드 **작업** 바둑판식으로 배열입니다.  이 인해 hello **작업** 블레이드에서 여기에서 클릭할 수 있습니다 hello 작업 레코드 tooview의 세부 정보 및 출력 하 고 있습니다.<br><br> ![Automation 계정 작업 블레이드](./media/automation-runbook-execution/automation-runbook-job-summary-blade.png)<br> 

### <a name="job-summary"></a>작업 요약
특정 runbook의 가장 최근 상태에 대해 생성 된 hello 작업의 모든 목록을 볼 수 있습니다. 작업 상태에 의해이 목록을 필터링 할 수 있습니다 및 hello hello에 대 한 날짜 범위 toohello 작업의 마지막 변경 내용이 있습니다. tooview의 세부 정보 및 출력을 작업의 hello 이름을 클릭 합니다. hello hello 작업의 자세히 보기 hello 값 포함 toothat 작업에 제공 된 hello runbook 매개 변수에 대 한 합니다.

Runbook에 대 한 tooview hello 작업 단계를 수행 하는 hello를 사용할 수 있습니다.

1. Hello Azure 포털에서에서 선택 **자동화** 자동화 계정의 hello 이름을 선택 합니다.
2. Hello 허브에서 선택 **Runbook** hello에서 **Runbook** 블레이드 hello 목록에서 runbook을 선택 합니다.
3. Hello 선택한 runbook에 대 한 hello 블레이드에서 hello 클릭 **작업** 바둑판식으로 배열입니다.
4. Hello 목록의 hello 작업 중 하나를 클릭 하 고 hello runbook 작업 세부 정보 블레이드에서 세부 정보 및 출력 볼 수 있습니다.

## <a name="retrieving-job-status-using-windows-powershell"></a>Windows PowerShell을 사용하여 작업 상태 검색
Hello를 사용할 수 있습니다 [Get AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) tooretrieve hello 작업 특정 작업의 runbook 및 hello 세부 정보를 생성 합니다. 사용 하 여 Windows PowerShell로 runbook을 시작 하는 경우 [시작 AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx), hello 결과 작업이 반환 됩니다. 사용 하 여 [Get AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx)출력 tooget 작업의 출력입니다.

hello 다음 명령 예제 hello 샘플 runbook에 대 한 마지막 작업을 검색 하 고 해당 상태, hello runbook 매개 변수에 대해 제공 되는 hello 값 및 hello hello 작업에서 출력 표시 합니다.

    $job = (Get-AzureRmAutomationJob –AutomationAccountName "MyAutomationAccount" `
    –RunbookName "Test-Runbook" -ResourceGroupName "ResourceGroup01" | sort LastModifiedDate –desc)[0]
    $job.Status
    $job.JobParameters
    Get-AzureRmAutomationJobOutput -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAcct" -Id $job.JobId –Stream Output

## <a name="fair-share"></a>공평 분배
순서 tooshare 리소스 hello 클라우드의 모든 runbook에서 Azure 자동화는 일시적으로 언로드 어떤 작업이 든 3 시간 동안 실행 된 후입니다.  이 시간 동안 [PowerShell 기반 runbook](automation-runbook-types.md#powershell-runbooks) 작업은 중지되며 다시 시작되지 않습니다.  작업 상태 표시 hello **Stopped**합니다.  이 형식의 runbook은 항상 후 다시 시작 hello 시작 부분에서 검사점을 지원 하지 않습니다.  

[PowerShell 워크플로 기반 Runbook](automation-runbook-types.md#powershell-workflow-runbooks)은 마지막 [검사점](https://docs.microsoft.com/system-center/sma/overview-powershell-workflows#bk_Checkpoints)에서 다시 시작됩니다.  3 시간을 실행 한 후 hello runbook 작업은 일시 중단 됩니다 hello 서비스 및 서버 인스턴스의 상태를 보여 줍니다 **실행, 리소스 대기**합니다.  샌드박스 사용 가능 해지면 hello runbook 자동으로 다시 시작 됩니다 hello 자동화 서비스 및 hello 마지막 검사점에서 다시 시작 합니다.  이것은 일시 중단/다시 시작에 대한 정상적인 PowerShell 워크플로 동작입니다.  Hello runbook 다시 초과 하면 런타임의 3 시간 hello 과정이 반복 toothree 시간.  Hello 세 번째 컴퓨터를 다시 시작 hello runbook 여전히 3 시간 내에 완료 되지 않은 다음 hello runbook 작업에 실패 하 고 hello 작업 상태가 표시 되 면 **실패, 리소스 대기**합니다.  이 경우 다음 hello 실패와 예외가 hello를 나타납니다.

*hello 작업 hello에서 반복적으로 제거 하기 때문에 실행을 계속할 수 없습니다 같은 검사점입니다. Runbook이 해당 상태를 유지하지 않고 시간이 오래 걸리는 작업을 수행하지 않는지 확인하세요.*

이 runbook 실행을 완료 하지 않고 무기한 tooprotect hello 서비스 수 toomake 되지 않는 것 다시 언로드되지 않으면 다음 검사점 toohello 합니다.

Hello 작업에 도달 하지 않은 hello 첫 번째 검사점 언로드되기 전에 hello runbook에 검사점이 없는 경우 다음 다시 시작 hello 처음부터 합니다.  

Runbook을 만들 때 해당 hello 시간 toorun 두 검사점 간에 어떤 작업도 3 시간을 초과 하지 않는지를 확인 해야 합니다. Tooadd 검사점 tooyour runbook tooensure 있는지 하거나 하지 않는이 3 시간 제한에 도달 장기 분할 해야 작업을 실행 합니다. 예를 들어 Runbook에서 대용량 SQL 데이터베이스의 인덱스를 다시 작성할 수 있습니다. 이 단일 작업이 공평 hello 안에 완료 되지 않으면 공유 제한 다음 hello 작업은 언로드되고 hello 처음부터 다시 시작 합니다. 이 경우 한 번에 테이블 하나씩 다시 인덱싱하는 등의 여러 단계를 hello 다시 인덱싱 작업을 중단 하 고 hello 작업 수를 다시 시작 후 마지막 작업 toocomplete hello 되도록 각 작업이 끝난 후 검사점을 삽입 해야 합니다.

## <a name="next-steps"></a>다음 단계
* Azure 자동화에서 runbook을 사용 하는 toostart 수 있는 hello 다른 메서드에 대 한 자세한 정보는 toolearn 참조 [Azure 자동화에서 runbook 시작](automation-starting-a-runbook.md)

