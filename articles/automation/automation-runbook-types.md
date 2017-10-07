---
title: "자동화 Runbook 형식 aaaAzure | Microsoft Docs"
description: "Azure 자동화 및 어떤 유형 toouse 결정할 때 고려해 야 하면 고려 사항에서 사용할 수 있는 runbook의 hello 다른 형식에 설명 합니다. "
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9265c975-4281-4819-a84f-d86641277f36
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/01/2017
ms.author: bwren
ms.openlocfilehash: c28aa57c77025764b16784372308a4ff2f596914
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-runbook-types"></a>Azure 자동화 Runbook 형식
Azure 자동화는 다음 표에 hello의 네 가지 유형의 간략하게 설명 하는 runbook 지원 합니다.  hello 아래 섹션에서는 추가 정보를 제공 될 때 고려 사항 포함 하 여 각 형식에 대 한 각 toouse 합니다.

| 형식 | 설명 |
|:--- |:--- |
| [그래픽](#graphical-runbooks) |Windows PowerShell을 기반으로 하며 Azure 포털의 그래픽 편집기로 완전하게 생성 및 편집됩니다. |
| [그래픽 PowerShell 워크플로](#graphical-runbooks) |Azure 포털에서 생성 되 고 완전 하 게 편집한 hello 그래픽 편집기 및 Windows PowerShell 워크플로 기반으로 합니다. |
| [PowerShell](#powershell-runbooks) |Windows PowerShell 스크립트를 기반으로 하는 텍스트 Runbook |
| [PowerShell 워크플로](#powershell-workflow-runbooks) |Windows PowerShell 워크플로를 기반으로 하는 텍스트 Runbook |

## <a name="graphical-runbooks"></a>그래픽 Runbook
[그래픽](automation-runbook-types.md#graphical-runbooks) 및 그래픽 PowerShell 워크플로 runbook에서 생성 되 고 hello hello Azure 포털의에서 그래픽 편집기로 편집 합니다.  Tooa 파일을 내보내야 하 고 다른 자동화 계정으로 가져올 수 있지만 만들거나 다른 도구로 편집할 수 없습니다.  그래픽 runbook에는 PowerShell 코드를 생성 하지만 직접 확인 하거나 hello 코드를 수정할 수 없습니다. 그래픽 runbook hello의 변환 된 tooone 안 [텍스트 형식](automation-runbook-types.md), 또는 텍스트 runbook 변환된 toographical 형식의 지정할 수 있습니다. 그래픽 runbook 가져오기 및 반대로 하는 동안 변환 된 tooGraphical PowerShell 워크플로 runbook 될 수 있습니다.

### <a name="advantages"></a>장점
* 시각적 삽입-링크-구성 제작 모델  
* Hello 프로세스를 통해 데이터 흐름에 집중  
* 관리 프로세스를 시각적으로 표시  
* 자식 runbook toocreate 높은 수준의 워크플로로 다른 runbook을 포함  
* 모듈식 프로그래밍 장려  


### <a name="limitations"></a>제한 사항
* Azure 포털 외부에서 Runbook을 편집할 수 없습니다.
* PowerShell 코드 tooperform 복잡 한 논리를 포함 하는 코드 작업을 할 수 있습니다.
* Hello 그래픽 워크플로 의해 만들어진 hello PowerShell 코드를 직접 편집 하거나 볼 수 없습니다. 참고 모든 코드 활동에서 생성 되는 hello 코드를 볼 수 있습니다.

## <a name="powershell-runbooks"></a>PowerShell Runbook
PowerShell Runbook은 Windows PowerShell을 기반으로 합니다.  직접 hello 텍스트 편집기를 사용 하 여 hello Azure 포털에서에서 하는 hello runbook의 hello 코드를 편집 합니다.  또한 오프 라인 텍스트 편집기를 사용할 수 있습니다 및 [hello runbook 가져오기](http://msdn.microsoft.com/library/azure/dn643637.aspx) Azure 자동화로 합니다.

### <a name="advantages"></a>장점
* PowerShell 워크플로 hello 추가 복잡성 없이 PowerShell 코드와 함께 모든 복잡 한 논리를 구현 합니다. 
* Runbook 실행 하기 전에 컴파일된 toobe 필요 하지 않습니다 이후 PowerShell 워크플로 runbook 보다 더 빨리 시작 합니다.

### <a name="limitations"></a>제한 사항
* PowerShell 스크립팅에 대해 잘 알아야 합니다.
* 사용할 수 없는 [병렬 처리](automation-powershell-workflow.md#parallel-processing) tooperform 병렬로 여러 동작 합니다.
* 사용할 수 없는 [검사점](automation-powershell-workflow.md#checkpoints) 오류 시 runbook tooresume 합니다.
* PowerShell 워크플로 runbook 및 그래픽 runbook만 포함할 수 자식 runbook으로 새 작업을 만듭니다는 hello Start-azureautomationrunbook cmdlet을 사용 하 여 합니다.

### <a name="known-issues"></a>알려진 문제
PowerShell Runbook에 대해 현재 알려진 문제는 다음과 같습니다.

* PowerShell Runbook은 null 값으로 암호화되지 않은 [변수 자산](automation-variables.md) 을 검색할 수 없습니다.
* PowerShell runbook을 검색할 수 없습니다는 [변수 자산](automation-variables.md) 와  *~*  hello 이름에서입니다.
* PowerShell Runbook의 반복적인 Get-Process는 80회 반복 후에 작동이 중단될 수 있습니다. 
* PowerShell runbook은 한 번에 매우 많은 양의 데이터 toohello 출력 스트림에 toowrite 시도 하는 경우 실패할 수 있습니다.   일반적으로 큰 개체로 작업할 때 필요한 hello 정보만 출력 하 여이 문제를 해결할 수 있습니다.  예를 들어 다음과 같이 출력 대신 *Get-process*, 방금 hello 필수 필드를 출력할 수 *Get-process | ProcessName, CPU 선택*합니다.

## <a name="powershell-workflow-runbooks"></a>PowerShell 워크플로 Runbook
PowerShell 워크플로 Runbook은 [Windows PowerShell 워크플로](automation-powershell-workflow.md)를 기반으로 하는 텍스트 Runbook입니다.  직접 hello 텍스트 편집기를 사용 하 여 hello Azure 포털에서에서 하는 hello runbook의 hello 코드를 편집 합니다.  또한 오프 라인 텍스트 편집기를 사용할 수 있습니다 및 [hello runbook 가져오기](http://msdn.microsoft.com/library/azure/dn643637.aspx) Azure 자동화로 합니다.

### <a name="advantages"></a>장점
* PowerShell 워크플로 코드로 모든 복잡한 로직을 구현합니다.
* 사용 하 여 [검사점](automation-powershell-workflow.md#checkpoints) 오류 시 runbook tooresume 합니다.
* 사용 하 여 [병렬 처리](automation-powershell-workflow.md#parallel-processing) tooperform 병렬로 여러 동작 합니다.
* 자식 runbook toocreate 높은 수준의 워크플로로 다른 그래픽 runbook 및 PowerShell 워크플로 runbook을 포함할 수 있습니다.

### <a name="limitations"></a>제한 사항
* 작성자는 PowerShell 워크플로를 잘 알아야 합니다.
* Runbook hello PowerShell 워크플로 복잡성이 추가 같은 처리 해야 [개체를 역직렬화 할](automation-powershell-workflow.md#code-changes)합니다.
* Runbook 실행 하기 전에 컴파일된 toobe 해야 하므로 PowerShell runbook 보다 더 긴 toostart를 사용 합니다.
* 새 작업을 만듭니다는 hello Start-azureautomationrunbook cmdlet을 사용 하 여 PowerShell runbook를 자식 runbook으로 포함할 수만 있습니다.

## <a name="considerations"></a>고려 사항
계정 hello 추가로 고려해 야 할 특정 runbook에 대 한 어떤 유형 toouse 결정할 때 다음을 고려해 야 합니다.

* 그래픽 tootextual 형식 또는 그 반대로에서 runbook을 변환할 수 없습니다.
* 형식이 다른 Runbook을 자식 Runbook으로 사용하는 경우 제한 사항이 있습니다.  자세한 내용은 [Azure 자동화의 자식 Runbook](automation-child-runbooks.md) 을 참조하세요.

## <a name="next-steps"></a>다음 단계
* 그래픽 runbook 제작에 대 한 더 toolearn 참조 [Azure 자동화의 그래픽 제작](automation-graphical-authoring-intro.md)
* toounderstand hello 차이점 PowerShell 및 PowerShell 워크플로 runbook에 대 한 자세한 내용은 [학습 Windows PowerShell 워크플로](automation-powershell-workflow.md)
* Toocreate 또는 가져오기 Runbook 참조 하는 방법에 대 한 자세한 내용은 [만들거나 Runbook 가져오기](automation-creating-importing-runbook.md)

