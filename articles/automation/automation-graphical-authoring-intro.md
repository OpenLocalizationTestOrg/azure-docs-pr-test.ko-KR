---
title: "aaaGraphical Azure 자동화에서 제작 | Microsoft Docs"
description: "그래픽 제작 하면 toocreate runbook Azure 자동화에 대 한 코드를 사용 합니다. 이 문서에서는 소개 toographical 제작 하 고 hello에 대 한 세부 정보를 모두 toostart 그래픽 runbook 만들기 필요 합니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 4b6f840c-e941-4293-a728-b33407317943
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/14/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 6ddf18b992d5e5f7f4af95f344007a63ac498549
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="graphical-authoring-in-azure-automation"></a>Azure 자동화에서 그래픽 작성
## <a name="introduction"></a>소개
그래픽 Authoring 있습니다 toocreate runbook을 Azure 자동화에 대 한 hello 기본 Windows PowerShell 또는 PowerShell 워크플로 코드의 복잡성을 hello 없이. 활동 toohello 캔버스 cmdlet 및 runbook의 라이브러리에서 함께 연결을 추가한 구성 tooform 워크플로 합니다.  System Center Orchestrator 나 SMA 서비스 관리 자동화 ()으로 계속 작업 하는 경우 다음이 표시 친숙 한 tooyou 됩니다.   

이 문서에서는 소개 toographical tooget 그래픽 runbook을 만드는 시작 해야 하는 제작 및 hello 개념을 제공 합니다.

## <a name="graphical-runbooks"></a>그래픽 Runbook
Azure 자동화의 모든 Runbook은 Windows PowerShell 워크플로입니다.  그래픽 및 그래픽 PowerShell 워크플로 runbook hello 자동화 작업 자가 실행 하는 PowerShell 코드를 생성 하지만 tooview 수 없는 것 있고 직접 수정할 수도 있습니다.  변환 된 tooa 그래픽 PowerShell 워크플로 runbook과 그 반대의 경우 그래픽 runbook 수는 있지만 변환된 tooa 텍스트 runbook 일 수 없습니다. 기존 텍스트 runbook hello 그래픽 편집기로 가져올 수 없습니다.  

## <a name="overview-of-graphical-editor"></a>그래픽 편집기 개요
Hello Azure 포털에서에서 만들거나 그래픽 runbook을 편집 하 여 hello 그래픽 편집기를 열 수 있습니다.

![그래픽 작업 영역](media/automation-graphical-authoring-intro/runbook-graphical-editor.png)

hello 다음 섹션에서는 컨트롤에 설명 hello hello 그래픽 편집기에서.

### <a name="canvas"></a>캔버스
hello 캔버스 runbook 디자인할입니다.  Hello 라이브러리 제어 toohello runbook의 hello 노드 모두에서 활동을 추가 하 고 hello runbook의 링크 toodefine hello 논리로 연결 합니다.

시작 및 종료 hello 컨트롤 hello 캔버스 toozoom hello 맨 아래에 사용할 수 있습니다.

![그래픽 작업 영역](media/automation-graphical-authoring-intro/runbook-canvas-controls.png)

### <a name="library-control"></a>라이브러리 컨트롤
hello 라이브러리 컨트롤은 선택할 수 있는 [활동](#activities) tooadd tooyour runbook입니다.  추가한 연결을 tooother 활동 toohello 캔버스입니다.  다음 표에 hello에 설명 된 4 개의 섹션을 포함 합니다.

| 섹션 | 설명 |
|:--- |:--- |
| Cmdlet |Runbook에서 사용할 수 있는 모든 hello cmdlet을 포함 합니다.  이러한 cmdlet은 모듈별로 구성됩니다.  모든 자동화 계정에서 설치 된 hello 모듈 사용할 수 있습니다. |
| Runbook |자동화 계정에 hello runbook을 포함합니다. 이러한 runbook toohello 캔버스 toobe 자식 runbook으로 사용 되는 추가할 수 있습니다. 유일한 runbook의 runbook을 편집 하 고 hello 대로 형식 핵심 동일 hello 표시 됩니다. 그래픽에 대 한 runbook PowerShell 기반 runbook 표시 된 그래픽 PowerShell 워크플로 runbook에 대해서만 PowerShell 워크플로 기반 runbook 표시 되어 있습니다. |
| 자산 |Hello 포함 [자동화 자산](http://msdn.microsoft.com/library/dn939988.aspx) runbook에서 사용할 수 있는 자동화 계정에서 합니다.  자산 tooa runbook을 추가 하는 경우 hello 선택한 자산을 가져옵니다.는 워크플로 활동을 추가 됩니다.  변수 자산 hello 경우에서 선택할 수 있습니다 tooadd 활동 tooget hello 변수 또는 설정 변수 hello 여부입니다. |
| Runbook 컨트롤 |현재 Runbook에서 사용할 수 있는 Runbook 컨트롤 활동을 포함합니다. A *접합* 여러 입력 하 고 모든 hello 워크플로 계속 하기 전에 완료 될 때까지 대기 합니다. A *코드* 활동 hello 그래픽 runbook 종류에 따라 PowerShell 또는 PowerShell 워크플로 코드의 하나 이상의 줄을 실행 합니다.  어려운 tooachieve 활동과 다른 활동은 기능 또는 사용자 지정 코드에 대 한이 작업을 사용할 수 있습니다. |

### <a name="configuration-control"></a>구성 컨트롤
hello 구성 제어 hello 캔버스에서 선택한 개체에 대 한 세부 정보 제공 됩니다. 이 컨트롤에 사용할 수 있는 hello 속성이 선택 된 개체의 hello 형식에 따라 달라 집니다.  Hello 구성 컨트롤에서에서 옵션을 선택 하는 경우 순서 tooprovide에 대 한 추가 정보에서 추가 블레이드가 열립니다.

### <a name="test-control"></a>테스트 컨트롤
hello 그래픽 편집기를 처음 시작할 때 hello 테스트 컨트롤 표시 되지 않습니다. 대화형으로 [그래픽 Runbook을 테스트](#graphical-runbook-procedures)할 때 열립니다.  

## <a name="graphical-runbook-procedures"></a>그래픽 Runbook 절차
### <a name="exporting-and-importing-a-graphical-runbook"></a>그래픽 Runbook 내보내기 및 가져오기
그래픽 runbook의 게시 된 버전 hello만 내보낼 수 있습니다.  Hello runbook 아직 게시 되지 않으면 다음 hello **게시 내보내기** 단추가 비활성화 됩니다.  Hello를 클릭할 때 **게시 내보내기** 단추, hello runbook은 로컬 컴퓨터에 다운로드 한 tooyour 합니다.  hello 이름이 hello 파일의 이름과 hello 사용 하 여 hello runbook의 한 *graphrunbook* 확장 합니다.

![게시된 항목 내보내기](media/automation-graphical-authoring-intro/runbook-export.png)

Hello를 선택 하 여 그래픽 또는 그래픽 PowerShell 워크플로 runbook 파일을 가져올 수 있습니다 **가져올** runbook을 추가 하는 경우 옵션입니다.   유지할 수 파일 tooimport hello를 선택 하면 동일한 hello **이름** 하거나 새 이름을 제공 합니다.  hello Runbook 유형 필드는 표시 하는 runbook의 hello 형식을 선택한 hello 파일 및 tooselect 잠재적 충돌 하 고 변환 하는 동안 있을 수는 메시지가 표시 됩니다 유효 하지 않은 다른 종류를 시도 하는 경우 평가 구문 오류가 발생 했습니다.  

![Runbook 가져오기](media/automation-graphical-authoring-intro/runbook-import-revised20165.png)

### <a name="testing-a-graphical-runbook"></a>그래픽 Runbook 테스트
버전 변경 하지 않은 hello runbook의 게시 된 hello를 종료 하거나 게시 하기 전에 새 runbook을 테스트할 수 있습니다 하는 동안 hello Azure 포털에서에서 runbook의 초안 버전을 hello를 테스트할 수 있습니다. 이렇게 하면 있습니다 tooverify runbook hello는 hello 게시 된 버전을 바꾸기 전에 제대로 작동 합니다. Runbook을 테스트할 때는 hello 초안 runbook 실행 되며 수행 하는 모든 작업이 완료 됩니다. 작업 기록은 만들어지지만 hello 테스트 출력 창에에서 출력이 표시 됩니다. 

편집 하기 위해 hello runbook을 열어 runbook에 대 한 hello 테스트 컨트롤을 열고 hello에 클릭 **테스트 창** 단추입니다.

![테스트 창 단추](media/automation-graphical-authoring-intro/runbook-edit-test-pane.png)

매개 변수를 입력 하 고 hello를 클릭 하 여 hello runbook을 시작할 수 있습니다에 대 한 hello 테스트 컨트롤 물어봅니다 **시작** 단추입니다.

![테스트 컨트롤 단추](media/automation-graphical-authoring-intro/runbook-test-start.png)

### <a name="publishing-a-graphical-runbook"></a>그래픽 Runbook 게시
Azure 자동화의 각 Runbook에는 초안 버전과 게시된 버전이 있습니다. Hello 게시 됨 버전만 실행 하는 사용 가능한 toobe 이며 hello 초안 버전만 편집할 수 있습니다. hello 게시 됨 버전이 모든 변경 내용 toohello 초안 버전의 영향을 받지 않습니다. 사용 가능한 준비 toobe hello 초안 버전을 사용 하는 경우 다음 게시 하면을 hello 초안 버전으로 hello 게시 됨 버전을 덮어씁니다.

편집 하 고 hello에서 클릭 하 여 hello runbook을 열어 그래픽 runbook을 게시할 수 있습니다 **게시** 단추입니다.

![게시 단추](media/automation-graphical-authoring-intro/runbook-edit-publish.png)

아직 게시하지 않은 Runbook은 상태가 **신규**입니다.  게시된 Runbook은 상태가 **게시됨**입니다.  Hello runbook의 상태에이 게시 되 고 hello 초안 버전과 게시 됨 버전은 다른 후 hello runbook을 편집 하는 경우 **편집에서**합니다.

![Runbook 상태](media/automation-graphical-authoring-intro/runbook-statuses-revised20165.png) 

Runbook의 hello 옵션 toorevert toohello 게시 됨 버전이 있습니다.  마지막으로 게시 하 고 hello 게시 됨 버전 hello runbook의 초안 버전 hello 교체 하는 hello runbook 이후의 변경 내용을 버리고 합니다.

![Toopublished 단추 되돌리기](media/automation-graphical-authoring-intro/runbook-edit-revert-published.png)

## <a name="activities"></a>활동
활동은 runbook의 hello 구성 요소입니다.  활동은 PowerShell cmdlet, 자식 Runbook 또는 워크플로 활동일 수 있습니다.  Hello 라이브러리 컨트롤에에서 클릭 마우스 오른쪽 단추로 선택 하 여 활동 toohello runbook을 추가 **toocanvas 추가**합니다.  그런 다음 클릭 하 고 hello 활동 tooplace를 캔버스 hello에 있는 모든 것을 끌면 수 있습니다.  hello hello 캔버스에 hello 활동의 hello 위치의 영향을 주지 않습니다 어떤 방식으로든에서 hello runbook의 hello 작동 합니다.  있습니다 수 레이아웃 runbook 가장 적합 한 toovisualize 찾을 작동 합니다. 

![Toocanvas 추가](media/automation-graphical-authoring-intro/add-to-canvas-revised20165.png)

Hello 구성 블레이드에서 hello 캔버스 tooconfigure에 hello 활동의 속성 및 매개 변수를 선택 합니다.  Hello를 변경할 수 있습니다 **레이블** 설명 tooyou는 hello 활동 toosomething입니다.  hello 원래 cmdlet 여전히 실행 되 고, 표시 이름 hello 그래픽 편집기에 사용 되는 변경할 수 있습니다.  hello 레이블 hello runbook 내에서 고유 해야 합니다. 

### <a name="parameter-sets"></a>매개 변수 집합
매개 변수 집합 hello 필수 및 선택적 매개 변수는 특정 cmdlet에 대 한 값을 허용 하를 정의 합니다.  모든 cmdlet에는 적어도 하나의 매개 변수 집합이 있으며, 여러 매개 변수 집합이 있는 cmdlet도 있습니다.  cmdlet에 여러 매개 변수 집합이 있는 경우 매개 변수를 구성하려면 먼저 사용할 매개 변수 집합을 선택해야 합니다.  구성할 수 있는 hello 매개 변수 선택 하는 hello 매개 변수 집합에 따라 달라 집니다.  Hello 매개 변수 집합을 선택 하 여 활동에서 사용 되는 변경할 수 있습니다 **매개 변수 설정** 다른 집합을 선택 하 고 있습니다.  이 경우 구성한 모든 매개 변수 값이 손실됩니다.

다음 예제는 hello, Get AzureRmVM hello cmdlet에는 세 가지 매개 변수 집합에 있습니다.  Hello 매개 변수 집합 중 하나를 선택할 때까지 매개 변수 값을 구성할 수 없습니다.  hello 매개 변수 집합을 ListVirtualMachineInResourceGroupParamSet 리소스 그룹의 모든 가상 컴퓨터를 반환 하는 데 있고 단일 선택적 매개 변수를 보유 합니다.  hello GetVirtualMachineInResourceGroupParamSet hello 가상 컴퓨터 tooreturn을 두 개의 필수 및 선택적 매개 변수 하나를 지정 하는입니다.

![매개 변수 집합](media/automation-graphical-authoring-intro/get-azurermvm-parameter-sets.png)

#### <a name="parameter-values"></a>매개 변수 값
매개 변수에 대해 값을 지정 하는 경우는 데이터 원본 toodetermine hello 값은 지정 하는 방법을 선택 합니다.  hello 데이터 원본에는 특정 매개 변수에 사용할 수 있는 hello 해당 매개 변수에 대해 유효한 값에 따라 달라 집니다.  예를 들어 Null은 null 값을 허용하지 않는 매개 변수에 사용 가능한 옵션이 아닙니다.

| 데이터 원본 | 설명 |
|:--- |:--- |
| 상수 값 |Hello 매개 변수에 대 한 값을 입력 합니다.  이 hello 다음 데이터 형식에 사용할 수만: Int32, Int64, String, Boolean, DateTime, 스위치입니다. |
| 활동 출력 |Hello 워크플로에서 hello 현재 활동 앞에 오는 활동에서 출력 합니다.  유효한 모든 활동이 나열됩니다.  방금 hello 활동 toouse hello 매개 변수 값에 대 한 출력을 선택 합니다.  Hello 활동 여러 속성을 가진 개체를 출력, 하는 경우 다음 입력할 수 있습니다 hello 속성의 hello 이름에 hello 활동을 선택한 후 합니다. |
| Runbook 입력 |활동 매개 변수 입력된 toohello로 runbook 입력된 매개 변수를 선택 합니다. |
| 변수 자산 |입력으로 자동화 변수를 선택합니다. |
| 자격 증명 자산 |입력으로 자동화 자격 증명을 선택합니다. |
| 인증서 자산 |입력으로 자동화 인증서를 선택합니다. |
| 연결 자산 |입력으로 자동화 연결을 선택합니다. |
| PowerShell 식 |간단한 [PowerShell 식](#powershell-expressions)을 지정합니다.  hello 식은 hello 활동과 hello 결과 hello 매개 변수 값에 사용 하기 전에 평가 됩니다.  활동 또는 runbook 입력된 매개 변수 toorefer toohello 출력을 사용할 수 있습니다. |
| 구성되지 않음 |이전에 구성된 모든 값을 지웁니다. |

#### <a name="optional-additional-parameters"></a>선택적 추가 매개 변수
모든 cmdlet hello 옵션 tooprovide 추가 매개 변수를 갖습니다.  이는 PowerShell 일반 매개 변수 또는 기타 사용자 지정 매개 변수입니다.  PowerShell 구문을 사용하여 매개 변수를 제공할 수 있는 텍스트 상자가 표시됩니다.  예를 들어 toouse hello **Verbose** 공통 매개 변수를 지정 하는 경우 **"-Verbose: $True"**합니다.

### <a name="retry-activity"></a>작업 다시 시도
**다시 시도 동작** 특정 조건이 충족 될 때까지 여러 번 실행 하는 활동 toobe 허용과 거의 동일한 루프입니다.  오류가 발생 하기 쉬우며, 여러 번 실행 해야 하는 작업에 대 한이 기능을 사용할 수 있고 필요 둘 이상의 성공에 시도 수도 테스트 유효한 데이터에 대 한 hello 활동의 hello 출력 정보.    

활동에 재시도 사용하면 지연 및 조건을 설정할 수 있습니다.  hello 지연은 hello 시간 (분 또는 초 단위) hello 활동을 다시 실행 하기 전에 해당 hello runbook 기다립니다.  지연 시간 없이 지정 된 경우 hello 활동은 다시 실행을 완료 한 후에 즉시. 

![작업 다시 시도 지연](media/automation-graphical-authoring-intro/retry-delay.png)

hello 다시 시도 조건에는 각 타임 hello 활동을 실행 한 후 계산 되는 PowerShell 식입니다.  Hello 식 tooTrue 확인 되 면 다음 hello 작업 다시 실행 합니다.  Hello 식 tooFalse 해결 되 면 hello 활동 않습니다 되지를 다시 실행 하 고 hello runbook toohello 다음 활동에서 이동 합니다. 

![작업 다시 시도 지연](media/automation-graphical-authoring-intro/retry-condition.png)

hello 다시 시도 조건 $RetryData hello 활동 재시도 대 한 액세스 tooinformation 제공 하 라는 변수를 사용할 수 있습니다.  이 변수 범위는 다음 표에 hello의 hello 속성입니다.

| 속성 | 설명 |
|:--- |:--- |
| NumberOfAttempts |수 hello 활동이 실행 된 횟수입니다. |
| 출력 |마지막 hello에서 출력으로 hello 활동의 실행 합니다. |
| TotalDuration |제한 시간이 hello 작업이 시작 된 이후 경과 처음으로 hello 합니다. |
| StartedAt |처음 시작 된 UTC 형식 hello 활동의 시간입니다. |

다음은 활동 다시 시도 조건의 예제입니다.

    # Run hello activity exactly 10 times.
    $RetryData.NumberOfAttempts -ge 10 

    # Run hello activity repeatedly until it produces any output.
    $RetryData.Output.Count -ge 1 

    # Run hello activity repeatedly until 2 minutes has elapsed. 
    $RetryData.TotalDuration.TotalMinutes -ge 2

Hello 활동 두 시각 신호 tooremind 포함 활동에 대 한 다시 시도 조건을 구성한 후 있습니다.  Hello 활동에 표시 된 하나 이며 다른 hello hello 활동의 hello 구성을 검토 합니다.

![작업 다시 시도 시각적 표시기](media/automation-graphical-authoring-intro/runbook-activity-retry-visual-cue.png)

### <a name="workflow-script-control"></a>워크플로 스크립트 컨트롤
코드 컨트롤은 그렇지 않은 경우 사용할 수 있는 주문 tooprovide 기능에서 작성 하는 그래픽 runbook의 hello 형식에 따라 PowerShell 또는 PowerShell 워크플로 스크립트를 허용 하는 특수 한 활동.  매개 변수를 사용할 수 없지만 활동 출력 및 Runbook 입력 매개 변수에 변수를 사용할 수는 있습니다.  Hello 활동의 출력이 toohello databus 없을 경우 대/소문자는 나가는 링크가 없는 자식이 추가 hello runbook의 toohello 출력 추가 됩니다.

예를 들어 hello 다음 코드 수행 $NumberOfDays 라는 runbook 입력된 변수를 사용 하 여 날짜 계산 합니다.  그런 다음 출력 toobe hello runbook의 이후 작업에서 사용으로 계산 된 날짜 시간을 보냅니다.

    $DateTimeNow = (Get-Date).ToUniversalTime()
    $DateTimeStart = ($DateTimeNow).AddDays(-$NumberOfDays)}
    $DateTimeStart


## <a name="links-and-workflow"></a>링크 및 워크플로
그래픽 Runbook의 **링크** 는 두 개의 활동을 연결합니다.  Hello 소스 활동 toohello 대상 활동에서 가리키는 화살표도 hello 캔버스에 표시 됩니다.  hello 활동 hello 화살표의 hello 방향의 hello 소스 활동이 완료 된 후 시작 하는 hello 대상 활동으로 실행 합니다.  

### <a name="create-a-link"></a>링크 만들기
Hello hello 셰이프의 맨 아래에 hello 원을 클릭 하 여 hello 소스 활동을 선택 하 여 두 활동 사이의 링크를 만듭니다.  Hello 화살표 toohello 대상 활동 및 릴리스를 끕니다.

![링크 만들기](media/automation-graphical-authoring-intro/create-link-revised20165.png)

Hello 구성 블레이드에서 hello 링크 tooconfigure 해당 속성을 선택 합니다.  다음 표에 hello에 설명 된 hello 링크 형식이 포함 됩니다.

| 링크 형식 | 설명 |
|:--- |:--- |
| 파이프라인 |hello 대상 활동 hello 소스 활동에서 각 개체 출력에 대해 한 번 실행 됩니다.  hello 소스 활동 결과 출력이 없는 경우에 hello 대상 활동이 실행 되지 않습니다.  Hello 소스 활동의 출력 개체로 제공 됩니다. |
| 시퀀스 |hello 대상 활동이 한 번만 실행 합니다.  개체의 배열을 hello 소스 활동에서 받습니다.  Hello 소스 활동의 출력 개체의 배열을로 제공 됩니다. |

### <a name="starting-activity"></a>시작 활동
그래픽 Runbook은 들어오는 링크가 없는 활동으로 시작됩니다.  이 역할을 hello hello runbook에 대 한 작업을 시작 하도록 하는 하나의 작업 종종 됩니다.  여러 활동에 들어오는 링크가 없는 경우에 병렬로 실행 하 여 hello runbook 시작 됩니다.  그 다음 따릅니다 hello 링크 toorun 다른 활동 각각 완료 합니다.

### <a name="conditions"></a>조건
링크에 조건을 지정 하면 hello 조건 tootrue 해결 되 면 hello 대상 활동이 실행만 않습니다.  일반적으로 hello 소스 활동에서 조건 tooretrieve hello 출력에는 $ActivityOutput 변수를 사용 합니다.  

파이프라인 링크에 대 한 단일 개체에 대 한 조건을 지정 하 고 hello 조건 hello 소스 활동에 의해 각 개체 출력에 대해 평가 됩니다.  그런 다음 hello 대상 활동 hello 조건을 만족 하는 각 개체에 대해 실행 됩니다.  예를 들어 Get AzureRmVm의 소스 활동으로 hello 구문 다음에 사용할 수는 조건부 파이프라인 링크 tooretrieve 가상 컴퓨터에 hello 라는 리소스 그룹에만 *Group1*합니다.  

    $ActivityOutput['Get Azure VMs'].Name -match "Group1"

시퀀스 링크에 대 한 hello 조건은 한 번만 계산 하므로 hello 소스 활동의 모든 개체 출력에 포함 된 단일 배열이 반환 됩니다.  이 때문에 시퀀스 링크는 파이프라인 링크 처럼 필터링에 사용할 수 없습니다만 hello 다음 활동의 실행 여부 확인 됩니다. 이 VM 시작 runbook의 작업 집합을 추적 하는 hello를 예로 들어 보겠습니다.<br> ![시퀀스와 조건부 링크](media/automation-graphical-authoring-intro/runbook-conditional-links-sequence.png)<br>
세 가지 서로 다른 시퀀스 링크 확인 하는 중 tootwo runbook 입력된 매개 변수 순서 toodetermine hello 적절 한 조치 tootake 인 리소스 그룹 이름 및 VM 이름을 나타내는 지정 된 값-단일 VM을 시작 하는, hello에서 모든 Vm을 시작 합니다. 리소스 그룹 또는 구독에 있는 모든 Vm입니다.  Hello 연결 tooAzure 및 Get 단일 VM 간의 링크를 시퀀스에 대 한 hello 조건 논리 다음과 같습니다.

    <# 
    Both VMName and ResourceGroupName runbook input parameters have values 
    #>
    (
    (($VMName -ne $null) -and ($VMName.Length -gt 0))
    ) -and (
    (($ResourceGroupName -ne $null) -and ($ResourceGroupName.Length -gt 0))
    )

조건부 링크를 사용 하는 경우 해당 분기에서 hello 소스 활동 tooother 활동에서 사용할 수 있는 hello 데이터 hello 조건에 따라 필터링 됩니다.  Hello 소스 toomultiple 링크 활동을 사용 하는 경우 데이터를 각 분기의 사용 가능한 tooactivities toothat 분기를 연결 하는 hello 링크의 hello 조건에 따라 달라 집니다 hello 합니다.

예를 들어 hello **시작 AzureRmVm** 아래 hello runbook의 작업 모든 가상 컴퓨터를 시작 합니다.  두 개의 조건부 링크가 있습니다.  첫 번째 조건부 링크 hello hello 식을 사용 하 여 *$ActivityOutput ['AzureRmVM 시작 ']. IsSuccessStatusCode-eq $true* toofilter hello 시작 AzureRmVm 활동 성공적으로 완료 합니다.  hello hello 식을 두 번째 사용 하 여 *$ActivityOutput ['AzureRmVM 시작 ']. IsSuccessStatusCode-ne $true* toofilter hello 시작 AzureRmVm 활동 toostart hello 가상 컴퓨터를 실패 한 경우.  

![조건부 링크 예제](media/automation-graphical-authoring-intro/runbook-conditional-links.png)

Hello 첫 번째 링크를 따르며 Get-azurevm에서 hello 활동 출력을 사용 하는 모든 작업이 Get-azurevm를 실행 하는 hello 시간에 시작 된 hello 가상 컴퓨터 받아볼 수만 있습니다.  두 번째 링크 hello 뒤에 오는 모든 활동 Get-azurevm를 실행 하는 hello 시 중지 되었던 hello hello 가상 컴퓨터 받아볼 수만 있습니다.  세 번째 페이지 hello 활동 상태에 관계 없이 실행 중인 모든 가상 컴퓨터를 받게 됩니다.

### <a name="junctions"></a>분기 동기화
분기 동기화는 들어오는 모든 분기가 완료될 때까지 대기하는 특별한 활동입니다.  이렇게 하면 toorun 병렬로 여러 활동 넘어가기 전에 모든 완료 되었는지 확인 합니다.

분기 동기화에서는 들어오는 링크의 개수에 제한이 없지만 이러한 링크가 두 개 이상이 아닌 경우에는 파이프라인일 수 있습니다.  들어오는 시퀀스 링크 hello 수는 제한 되지 않습니다.  여러 들어오는 파이프라인 링크가 있는 toocreate hello 접합 허용할 및 hello runbook을 저장 하지만 실행 하는 경우 실패 합니다.

다음 예제에서는 hello toothose 컴퓨터 적용 패치 toobe를 동시에 다운로드 하는 동안 가상 컴퓨터의 집합을 시작 하는 runbook의 일부입니다.  교차점 사용 되는 tooensure은 두 프로세스가 완료 된 후에 hello runbook을 계속 합니다.

![분기 동기화](media/automation-graphical-authoring-intro/runbook-junction.png)

### <a name="cycles"></a>주기
사이클은 대상 활동 다시 연결 되 면 tooits 소스는 결국 다시 연결 tooits 소스 활동 또는 tooanother 활동입니다.  주기는 그래픽 작성에서 현재 허용되지 않습니다.  Runbook에 주기가 있는 경우 정상적으로 저장되지만 실행하면 오류가 발생합니다.

![주기](media/automation-graphical-authoring-intro/runbook-cycle.png)

### <a name="sharing-data-between-activities"></a>활동 간의 데이터 공유
모든 데이터를 보내는 링크와 관련 된 활동에서 출력 된 toohello 쓰여집니다 *databus* hello runbook에 대 한 합니다.  Hello runbook의 모든 작업 hello databus toopopulate 매개 변수 값에 데이터를 사용 하거나 스크립트 코드에 포함할 수 있습니다.  활동은 hello 워크플로의 모든 이전 작업의 출력을 hello 액세스할 수 있습니다.     

Hello 데이터 toohello databus 쓰여지는 방법을 hello 유형의 hello 활동에 대 한 링크에 따라 달라 집니다.  에 대 한는 **파이프라인**, hello 데이터는 여러 개의 차트 개체로 출력 합니다.  에 대 한는 **시퀀스** 링크를 hello 데이터는 출력 배열입니다.  값이 하나만 있으면 단일 요소 배열로 출력됩니다.

두 가지 방법 중 하나를 사용 하 여 hello databus에 데이터를 액세스할 수 있습니다.  처음 사용 하는 프로그램 **활동 출력** 데이터 원본 toopopulate 다른 활동의 매개 변수입니다.  개체 hello 출력을 사용 하는 경우에 단일 속성을 지정할 수 있습니다.

![활동 출력](media/automation-graphical-authoring-intro/activity-output-datasource-revised20165.png)

Hello 출력에 있는 활동을 검색할 수도 있습니다는 **PowerShell 식을** 데이터 원본 또는 **워크플로 스크립트** ActivityOutput 변수와 함께 작업 합니다.  개체 hello 출력을 사용 하는 경우에 단일 속성을 지정할 수 있습니다.  ActivityOutput 변수 구문 다음 hello를 사용 합니다.

    $ActivityOutput['Activity Label']
    $ActivityOutput['Activity Label'].PropertyName 

### <a name="checkpoints"></a>검사점
작업에서 [검사점 Runbook](automation-powershell-workflow.md#checkpoints) 을 선택하여 그래픽 PowerShell 워크플로 Runbook에서 *검사점* 을 설정할 수 있습니다.  이렇게 하면 hello 활동을 실행 한 후 설정 검사점 toobe 됩니다.

![검사점](media/automation-graphical-authoring-intro/set-checkpoint.png)

검사점은 그래픽 PowerShell 워크플로 runbook에서 사용할 수 있고 그래픽 runbook에서는 사용할 수 없습니다.  Hello runbook이 일시 중지 및 다시 시작 되는 경우에 추가 AzureRMAccount 인 검사 모든 작업 hello runbook이 Azure cmdlet을 사용 하는 경우 수행 해야 다른 작업자에 대해이 검사점에서 합니다. 

## <a name="authenticating-tooazure-resources"></a>인증 tooAzure 리소스
Azure 리소스를 관리 하는 Azure 자동화의 Runbook 인증 tooAzure 필요 합니다.  hello [실행 계정을](automation-offering-get-started.md#creating-an-automation-account) (또한: 참조 된 tooas 서비스 사용자)는 hello 기본 메서드 tooaccess 자동화 runbook으로 구독에서 Azure 리소스 관리자 리소스입니다.  Hello를 추가 하 여이 기능 tooa 그래픽 runbook을 추가할 수 있습니다 **AzureRunAsConnection** PowerShell hello를 사용 하는 연결 자산 [Get-automationconnection](https://technet.microsoft.com/library/dn919922%28v=sc.16%29.aspx) cmdlet 및 [추가 AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet toohello 캔버스입니다. 다음 예제는 hello에 설명 되어 있습니다.<br>![실행 인증 작업](media/automation-graphical-authoring-intro/authenticate-run-as-account.png)<br>
hello 실행으로 연결 가져오기 작업 (예: Get-automationconnection), AzureRunAsConnection 라는 상수 값 데이터 원본으로 구성 됩니다.<br>![실행 연결 구성](media/automation-graphical-authoring-intro/authenticate-runas-parameterset.png)<br>
hello 다음 활동 추가-AzureRmAccount hello 인증에 사용할 실행 계정을 사용 하 여 hello runbook에 추가 합니다.<br>
![Add-AzureRmAccount 매개 변수 집합](media/automation-graphical-authoring-intro/authenticate-conn-to-azure-parameter-set.png)<br>
Hello 매개 변수에 대 한 **APPLICATIONID**, **CERTIFICATETHUMBPRINT**, 및 **TENANTID** 때문에 hello 필드 경로 hello 속성의 toospecify hello 이름이 필요 합니다 hello 활동 여러 속성을 가진 개체를 출력합니다.  그렇지 않으면 hello runbook를 실행 해도 오류가 tooauthenticate를 실패 합니다.  이 hello로 runbook 계정으로 실행 하는 최소 tooauthenticate에 필요한 것입니다.

toomaintain 이전 버전과 호환성 자동화를 작성 한 구독자에 대해 사용 하 여 계정을 [Azure AD 사용자 계정을](automation-create-aduser-account.md) toomanage Azure 클래식 배포 또는 Azure 리소스 관리자 리소스에 대 한 메서드 tooauthenticate 환영 사용 하 여 hello Add-azureaccount cmdlet은 한 [자격 증명 자산](automation-credentials.md) 액세스 toohello Azure 계정 사용 하는 Active Directory 사용자를 나타내는입니다.

Add-azureaccount 활동 뒤에 자격 증명 자산 toohello 캔버스에 추가 하 여이 기능 tooa 그래픽 runbook을 추가할 수 있습니다.  추가 AzureAccount hello 자격 증명 활동을 사용 하 여 해당 입력에 대 한 합니다.  다음 예제는 hello에 설명 되어 있습니다.

![인증 활동](media/automation-graphical-authoring-intro/authentication-activities.png)

Hello 시작 hello runbook의과 각 검사점 뒤에 tooauthenticate를 포함합니다.  즉, 모든 Checkpoint-Workflow 활동 뒤에 Add-AzureAccount 활동을 추가해야 합니다. 추가 자격 증명 필요 하지 않으면 활동을 사용할 수 있으므로 동일한 hello 

![활동 출력](media/automation-graphical-authoring-intro/authentication-activity-output.png)

## <a name="runbook-input-and-output"></a>Runbook 입력 및 출력
### <a name="runbook-input"></a>Runbook 입력
Hello 현재 자식으로 사용 되는 경우 hello Azure 포털을 통해 또는 다른 runbook에서 hello runbook을 시작할 때 runbook에서 확인 하는 사용자 입력을 필요할 수 있습니다.
예를 들어 runbook이 가상 컴퓨터를 만드는 경우 해야 hello 가상 컴퓨터의 hello 이름과 같은 tooprovide 정보 및 기타 속성 hello runbook을 시작할 때마다 합니다.  

하나 이상의 입력 매개 변수를 정의하여 Runbook에 대한 입력을 허용합니다.  각 시간 hello runbook을 시작 하는 이러한 매개 변수에 대해 값을 제공 합니다.  Azure 포털 hello로 runbook을 시작할 때 물어봅니다 tooprovide 각 hello hello runbook의 입력된 매개 변수의 값입니다.

Hello를 클릭 하 여 runbook에 대 한 입력된 매개 변수를 액세스할 수 있습니다 **입력 및 출력** hello runbook 도구 모음에서 단추입니다.  

![Runbook 입력 및 출력](media/automation-graphical-authoring-intro/runbook-edit-input-output.png) 

Hello 열립니다 **입력 및 출력** 기존 입력된 매개 변수를 편집 하거나 새를 클릭 하 여 만들 수 있는 컨트롤 **입력 추가**합니다. 

![입력 추가](media/automation-graphical-authoring-intro/runbook-edit-add-input.png)

각 입력된 매개 변수는 hello 속성 hello 표 다음에 의해 정의 됩니다.

| 속성 | 설명 |
|:--- |:--- |
| 이름 |hello hello 매개 변수의 고유 이름입니다.  영숫자 문자만 포함할 수 있으며, 공백을 포함할 수 없습니다. |
| 설명 |입력된 매개 변수 hello에 대 한 선택적 설명입니다. |
| 형식 |Hello 매개 변수 값에 대 한 예상 데이터 형식입니다.  Azure 포털 hello 입력 메시지를 표시 하는 경우 각 매개 변수에 대해 hello 데이터 형식에 대 한 적절 한 컨트롤을 제공 합니다. |
| 필수 |Hello 매개 변수에 대 한 값을 제공 해야 하는지 여부를 지정 합니다.  기본값이 정의 되지 않은 각 필수 매개 변수에 대해 값을 제공 하지 않으면 hello runbook은 시작할 수 없습니다. |
| 기본값 |어떤 값이 제공 되지 않은 경우 hello 매개 변수에 대 한 사용을 지정 합니다.  Null 또는 특정 값일 수 있습니다. |

### <a name="runbook-output"></a>Runbook 출력
나가는 링크가 없는 모든 활동에 의해 생성 된 데이터를 추가할 toohello [hello runbook의 출력](http://msdn.microsoft.com/library/azure/dn879148.aspx)합니다.  hello 출력 hello runbook 작업과 저장 되 고 hello runbook은 자식으로 사용 될 때 사용할 수 있는 tooa 부모 runbook 됩니다.  

## <a name="powershell-expressions"></a>PowerShell 식
그래픽 제작 hello 장점 중 하나에 게 제공 하면 hello 기능 toobuild powershell 지식이 별로 없더라도 runbook입니다.  현재 필요가 tooknow 약간 PowerShell의 특정를 채우기 위한 있지만 [매개 변수 값](#activities) 및 설정에 대 한 [조건을 연결](#links-and-workflow)합니다.  이 섹션 tooPowerShell 식에 대 한 있을 수 있는 해당 사용자에 대 한 간략 한 소개를 제공 합니다.  PowerShell의 세부 사항 전체는 [Windows PowerShell을 사용하는 스크립트](http://technet.microsoft.com/library/bb978526.aspx)에서 사용 가능합니다. 

### <a name="powershell-expression-data-source"></a>PowerShell 식 데이터 원본
PowerShell 식의 데이터 원본 toopopulate hello 값으로 사용할 수 있습니다는 [활동 매개 변수](#activities) hello 결과 일부 PowerShell 코드를 사용 합니다.  간단한 함수를 수행하는 코드 한 줄이거나 또는 복잡한 함수를 수행하는 여러 줄의 코드일 수 있습니다.  하지 않은 명령에서 모든 출력은 tooa 할당 변수는 출력 toohello 매개 변수 값입니다. 

예를 들어 다음 명령을 hello hello 현재 날짜 출력 됩니다. 

    Get-Date

hello 다음 명령은 현재 날짜 hello에서 문자열을 작성할를 tooa 변수 할당.  hello 변수의 hello 내용은 toohello 출력을 보내집니다. 

    $string = "hello current date is " + (Get-Date)
    $string

hello 다음 명령을 hello 현재 날짜를 평가 하 고 인지를 나타내는 hello 현재 날짜 주말 또는 평일 문자열을 반환 합니다. 

    $date = Get-Date
    if (($date.DayOfWeek = "Saturday") -or ($date.DayOfWeek = "Sunday")) { "Weekend" }
    else { "Weekday" }


### <a name="activity-output"></a>활동 출력
hello runbook, 구문 다음 hello로 hello $ActivityOutput 변수 사용의에서 이전 작업에서 toouse hello 출력 합니다.

    $ActivityOutput['Activity Label'].PropertyName

예를 들어 가상 컴퓨터의 hello 이름을 요구 하는 속성을 가진 활동 있을 경우 다음 식은 hello를 사용할 수 있습니다.

    $ActivityOutput['Get-AzureVm'].Name

방금 속성을 다음 대신 hello 가상 컴퓨터 개체를 필요한 hello 속성은 반환 하는 경우 구문 다음 hello hello 전체 개체를 사용 하 여 합니다.

    $ActivityOutput['Get-AzureVm']

또한 텍스트 toohello 가상 컴퓨터 이름을 연결 하는 hello 다음과 같은 보다 복잡 한 식에서 활동 hello 출력을 사용할 수 있습니다.

    "hello computer name is " + $ActivityOutput['Get-AzureVm'].Name


### <a name="conditions"></a>조건
사용 하 여 [비교 연산자](https://technet.microsoft.com/library/hh847759.aspx) toocompare 값 또는 값에 지정된 된 패턴과 일치 하는지 확인 합니다.  비교는 $true 또는 $false의 값을 반환합니다.

예를 들어 다음 조건 hello 활동에서 hello 가상 컴퓨터 이름을 지정 여부를 결정 *Get-azurevm* 현재 *중지*합니다. 

    $ActivityOutput["Get-AzureVM"].PowerState –eq "Stopped"

hello 같은 hello 동일한 가상 컴퓨터 상태 인지 여부를 모든 이외의 검사 조건 *중지*합니다.

    $ActivityOutput["Get-AzureVM"].PowerState –ne "Stopped"

**-and** 또는 **-or**와 같은 [논리 연산자](https://technet.microsoft.com/library/hh847789.aspx)를 사용하여 여러 조건을 조인할 수 있습니다.  인지 hello hello 이전 예제에서 동일한 가상 컴퓨터의 상태에 hello 다음 검사 조건 예를 들어 *중지* 또는 *중지*합니다.

    ($ActivityOutput["Get-AzureVM"].PowerState –eq "Stopped") -or ($ActivityOutput["Get-AzureVM"].PowerState –eq "Stopping") 


### <a name="hashtables"></a>해시 테이블
[해시 테이블](http://technet.microsoft.com/library/hh847780.aspx) 은 값 집합을 반환하는 데 유용한 이름/값 쌍입니다.  특정 활동에 대한 속성은 단순 값 대신 해시 테이블을 필요로 할 수 있습니다.  해시 테이블 참조 tooas 사전 표시 될 수 있습니다. 

구문 다음 hello로 해시 테이블을 만듭니다.  해시 테이블은 항목을 몇 개이든 포함할 수 있지만 각각은 이름 및 값으로 정의됩니다.

    @{ <name> = <value>; [<name> = <value> ] ...}

예를 들어 hello 다음 식은 만듭니다 인터넷 검색에 대 한 값으로 해시 테이블을 예상 하는 활동 매개 변수에서 hello 데이터 원본에에서 사용 되는 해시 테이블 toobe 합니다.

    $query = "Azure Automation"
    $count = 10
    $h = @{'q'=$query; 'lr'='lang_ja';  'count'=$Count}
    $h

hello 다음 예제에서는 호출 작업의 출력 *Twitter 연결 가져오기* toopopulate 해시 테이블입니다.

    @{'ApiKey'=$ActivityOutput['Get Twitter Connection'].ConsumerAPIKey;
      'ApiSecret'=$ActivityOutput['Get Twitter Connection'].ConsumerAPISecret;
      'AccessToken'=$ActivityOutput['Get Twitter Connection'].AccessToken;
      'AccessTokenSecret'=$ActivityOutput['Get Twitter Connection'].AccessTokenSecret}



## <a name="next-steps"></a>다음 단계
* PowerShell 워크플로 runbook 시작 tooget 참조 [내 첫 번째 PowerShell 워크플로 runbook](automation-first-runbook-textual.md) 
* 그래픽 runbook 시작 tooget 참조 [내 첫 번째 그래픽 runbook](automation-first-runbook-graphical.md)
* runbook 형식이, 장점 및 제한 사항에 대해 자세히 tooknow 참조 [Azure 자동화 runbook 형식](automation-runbook-types.md)
* toounderstand 자동화 계정으로 실행 계정 hello tooauthenticate를 사용 하 여 참조 [구성할 Azure 실행 계정](automation-sec-configure-azure-runas-account.md)

