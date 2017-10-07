---
title: "Azure 자동화의 runbook aaaChild | Microsoft Docs"
description: "다른 runbook에서 Azure 자동화에서 runbook을 시작 하 고 서로 정보를 공유 hello 다른 방법을 설명 합니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 919887b9-43e2-4c16-883c-f81807fe37db
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2017
ms.author: magoedte;bwren
ms.openlocfilehash: d3d06818d344b565d53cc4f4705b41dcfcf9a376
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="child-runbooks-in-azure-automation"></a>Azure 자동화의 자식 runbook
Azure 자동화 toowrite 재사용 가능한 모듈식 runbook 다른 runbook에서 사용할 수 있는 이산 함수 사용에 것이 좋습니다. 부모 runbook은 종종 하나 이상의 자식 runbook을 호출 tooperform 필수 기능입니다. 두 가지 방법으로 toocall 자식 runbook 있으며 각각에 서로 다른 특징을 이해 해야 하는 다양 한 시나리오에 대 한 최상의 될 결정할 수 있도록 합니다.

## <a name="invoking-a-child-runbook-using-inline-execution"></a>인라인 실행을 사용하여 자식 runbook 호출
tooinvoke 인라인으로 runbook 다른 runbook에서 hello runbook의 hello 이름을 사용 하 고이 활동이 나 cmdlet을 사용할 때와 정확히 해당 매개 변수의 값을 제공 합니다.  모든 runbook에서 같은 자동화 계정의 hello도 사용할 수 있는 tooall toobe이 방식이으로 사용해 서 키워드가 있습니다. hello 부모 runbook은 toohello 다음 줄을 이동 하기 전에 자식 runbook toocomplete hello에 대 한 대기 하 고 어떤 출력도 직접 toohello 부모 반환 됩니다.

인라인으로 runbook을 호출 하면 hello hello 부모 runbook과 같은 작업에서 실행 됩니다. Hello 자식 runbook이 실행의 hello 작업 기록은 표시 되지 됩니다. 모든 예외와 스트림 hello 자식 runbook에서 출력 hello 부모와 연결 됩니다. 이 따라서 작업 수가 감소 및 hello 자식 runbook에서 throw 된 예외가 이후 tootrack 쉽고 tootroubleshoot 유용 하 고의 모든 스트림 출력이 hello 부모 작업과 연결 합니다.

runbook이 게시되면 호출하는 모든 자식 runbook은 이미 게시되어야 합니다. runbook이 컴파일될 때 Azure 자동화가 모든 자식 runbook과 연결을 빌드하기 때문입니다. 그렇지 않은 경우 hello 부모 runbook은 toopublish 적절 하 게 나타나지만 시작 될 때 예외가 발생 합니다. 이 경우 순서 tooproperly 참조 hello 자식 runbook의 hello 부모 runbook을 다시 게시할 수 있습니다. Hello 자식 runbook이 변경 되어도 hello 연결이 이미 되었습니다 작성 하는 경우 toorepublish hello 부모 runbook이 필요 하지 않습니다.

인라인으로 호출 하는 자식 runbook의 hello 매개 변수에는 복잡 한 개체를 비롯 한 모든 데이터 형식일 수 있으며는 없는 [JSON serialization](automation-starting-a-runbook.md#runbook-parameters) hello Azure 관리 포털을 사용 하 여 hello runbook을 시작할 때 이나 hello로 시작 AzureRmAutomationRunbook cmdlet을 사용 합니다.

### <a name="runbook-types"></a>Runbook 형식
서로를 호출할 수 있는 형식:

* [PowerShell runbook](automation-runbook-types.md#powershell-runbooks) 및 [Graphical runbook](automation-runbook-types.md#graphical-runbooks)은 인라인으로 서로를 호출할 수 있습니다(둘 다 PowerShell 기반임).
* [PowerShell 워크플로 Runbook](automation-runbook-types.md#powershell-workflow-runbooks) 및 그래픽 PowerShell 워크플로 Runbook은 인라인으로 서로를 호출할 수 있습니다(둘 다 PowerShell 워크플로 기반임).
* PowerShell 형식 hello 및 PowerShell 워크플로 형식을 hello 서로 인라인을 호출할 수 없습니다 시작 AzureRmAutomationRunbook를 사용 해야 합니다.

게시 순서가 중요한 경우:

* hello의 순서가 runbook만 중요 PowerShell 워크플로 및 그래픽 PowerShell 워크플로 runbook에 대 한 게시 합니다.

인라인 실행을 사용 하 여 그래픽 또는 PowerShell 워크플로 자식 runbook을 호출할 때 hello hello runbook 이름을 사용할 것입니다.  PowerShell 자식 runbook을 호출할 때 사용 하 여 이름을 오는 *.\\*  스크립트 hello toospecify hello 로컬 디렉터리에 위치 합니다. 

### <a name="example"></a>예제
다음 예제는 hello 세 개의 매개 변수, 복잡 한 개체, 정수 및 부울 값을 허용 하는 테스트 자식 runbook을 호출 합니다. hello 자식 runbook의 hello 출력 tooa 변수에 할당 됩니다.  이 경우 hello 자식 runbook은 PowerShell 워크플로 runbook

    $vm = Get-AzureRmVM –ResourceGroupName "LabRG" –Name "MyVM"
    $output = PSWF-ChildRunbook –VM $vm –RepeatCount 2 –Restart $true

다음은 hello PowerShell runbook을 사용 하 여 hello 자식으로 동일한 예입니다.

    $vm = Get-AzureRmVM –ResourceGroupName "LabRG" –Name "MyVM"
    $output = .\PS-ChildRunbook.ps1 –VM $vm –RepeatCount 2 –Restart $true


## <a name="starting-a-child-runbook-using-cmdlet"></a>cmdlet을 사용하여 자식 runbook 시작
Hello를 사용할 수 있습니다 [시작 AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) cmdlet toostart에 설명 된 대로 runbook [toostart Windows PowerShell로 runbook](automation-starting-a-runbook.md#starting-a-runbook-with-windows-powershell)합니다. 이 cmdlet에 사용할 두 가지 모드가 있습니다.  하나의 모드로 hello cmdlet hello 자식 runbook에 대해 hello 자식 작업이 만들어지는 즉시 hello 작업 id를 반환 합니다.  Hello hello를 지정 하 여 사용할 수 있는 다른 모드에서 **-대기** 매개 변수를 hello cmdlet hello 자식 될 때까지 대기 작업이 완료 될 하 고 hello 출력 hello 자식 runbook에서 반환 됩니다.

cmdlet으로 시작 하는 자식 runbook에서 작업을 hello hello 부모 runbook에서 별도 작업에서 실행 됩니다. 이 작업이 hello 인라인으로 runbook을 호출 하는 보다 이며 더 어렵게 tootrack 유용 합니다. hello 부모는 각 toocomplete까지 기다리지 않고 여러 자식 runbook 작업을 비동기적으로 시작할 수 있습니다. 같은 종류의 hello 자식 runbook을 인라인으로 호출 하는 병렬 실행을에 대 한 hello 부모 runbook toouse hello 필요 [병렬 키워드](automation-powershell-workflow.md#parallel-processing)합니다.

[Runbook 매개 변수](automation-starting-a-runbook.md#runbook-parameters)에서 설명한 대로 cmdlet을 사용하여 시작된 자식 Runbook에 대한 매개 변수는 해시 테이블로 제공됩니다. 단순한 데이터 형식만 사용할 수 있습니다. Hello runbook은 복잡 한 데이터 형식과 매개 변수를 다음 그 인라인으로 호출 해야 합니다.

### <a name="example"></a>예제
hello 다음 예제에서는 시작 하는 자식 runbook 매개 변수 및 다음 기다립니다 toocomplete 시작 AzureRmAutomationRunbook hello를 사용 하 여-매개 변수를 대기 합니다. 완료 되 면 hello 자식 runbook에서 해당 출력을 수집 합니다.

    $params = @{"VMName"="MyVM";"RepeatCount"=2;"Restart"=$true} 
    $joboutput = Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-ChildRunbook" -ResourceGroupName "LabRG" –Parameters $params –wait


## <a name="comparison-of-methods-for-calling-a-child-runbook"></a>자식 runbook을 호출하기 위한 방법 비교
hello 다음 표에 요약 되어 다른 runbook에서 runbook을 호출 하는 것에 대 한 hello 두 방법 간의 hello 차이점이 있습니다.

|  | 인라인 | Cmdlet |
|:--- |:--- |:--- |
| 작업 |자식 runbook hello hello 부모와 동일한 작업에서 실행 합니다. |Hello 자식 runbook에 대해 별도 작업이 만들어집니다. |
| 실행 |부모 runbook은 계속 하기 전에 자식 runbook toocomplete hello에 대 한 대기합니다. |자식 runbook이 시작 된 후에 즉시 부모 runbook을 계속 *또는* 부모 runbook이 자식 작업 toofinish hello에 대 한 대기 합니다. |
| 출력 |부모 runbook은 자식 runbook에서 출력을 직접 가져올 수 있습니다. |부모 Runbook은 자식 Runbook 작업에서 출력을 검색하거나 *또는* 자식 Runbook에서 출력을 직접 가져올 수 있습니다. |
| 매개 변수 |Hello 자식 runbook 매개 변수의 값은 별도로 지정 되며 및 모든 데이터 형식을 사용할 수 있습니다. |Hello 자식 runbook 매개 변수는 단일 해시 테이블에 결합 해야 하며 단순 하 고 포함할 수 있습니다에 대 한 값 배열 및 데이터 형식을 JSON serialization을 사용 하는 개체입니다. |
| 자동화 계정 |부모 runbook hello에 자식 runbook만 사용할 수 같은 자동화 계정의 합니다. |부모 runbook hello에서 모든 자동화 계정에서 자식 runbook צ ְ ײ 동일한 Azure 구독과 연결 tooit 있으면도 다른 구독 합니다. |
| 게시 |부모 runbook을 게시하기 전에 자식 runbook을 게시해야 합니다. |부모 runbook을 시작하기 전 언제든 자식 runbook을 게시해야 합니다. |

## <a name="next-steps"></a>다음 단계
* [Azure 자동화에서 Runbook 시작](automation-starting-a-runbook.md)
* [Azure 자동화에서 Runbook 출력 및 메시지](automation-runbook-output-and-messages.md)

