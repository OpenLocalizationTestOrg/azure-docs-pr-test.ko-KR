---
title: "Azure 자동화의 그래픽 runbook에서 처리 aaaError | Microsoft Docs"
description: "이 문서에서는 설명 방법을 tooimplement 오류 Azure 자동화의 그래픽 runbook에서 논리를 처리 합니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/26/2016
ms.author: magoedte
ms.openlocfilehash: b9ff01361d2ebd9c0174b074a7a290b1cc2fd1c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="error-handling-in-azure-automation-graphical-runbooks"></a>Azure Automation 그래픽 runbook의 오류 처리

Runbook 경험할 수 있는 다른 문제를 식별 하는 키 runbook 디자인 주 tooconsider입니다. 이러한 문제는 성공, 예상된 오류 상태 및 예기치 않은 오류 조건을 포함할 수 있습니다.

runbook은 오류 처리를 포함해야 합니다. toovalidate 활동 출력 hello 또는 그래픽 runbook으로 오류를 처리, Windows PowerShell 코드 활동을 사용 하 여, hello 활동의 출력 링크 hello에 조건부 논리를 정의 하거나 다른 방법을 적용할 수 있습니다.          

종종 runbook 작업으로 발생 하는 종료 되지 않는 오류 이면 뒤에 오는 모든 활동 hello 오류에 관계 없이 처리 됩니다. hello 오류는 가능성이 toogenerate 예외가 있지만 hello 다음 활동 toorun 여전히 허용 됩니다. PowerShell은 설계 된 toohandle 오류는 hello 방법입니다.    

실행 하는 동안 발생할 수 있는 PowerShell 오류 hello 유형의 종료 또는 종료 되지 않는 됩니다. 종료 및 종료 되지 않는 오류 hello 차이점은 다음과 같습니다.

* **종료 오류**: hello 명령 (또는 스크립트 실행)을 완전히 중단 실행 하는 동안 심각한 오류가 있습니다. 예를 들어 존재하지 않는 cmdlet, cmdlet을 실행하지 못하도록 하는 구문 오류 또는 기타 심각한 오류를 포함합니다.

* **종료 되지 않는 오류**: hello 오류 불구 하 고 실행 toocontinue 허용 하는 비 심각한 오류가 있습니다. 예를 들어 찾을 수 없는 파일 오류 및 권한 문제 등의 작동 오류가 있습니다.

Azure 자동화의 그래픽 runbook으로 hello 기능 tooinclude 오류 처리 개선 되었습니다. 이제 예외를 종료되지 않는 오류로 전환하고 활동 간에 오류 링크를 만들 수 있습니다. 이 프로세스는 runbook 제작자 toocatch 오류 수 하 고 실현 또는 예기치 않은 상태를 관리 합니다.  

## <a name="when-toouse-error-handling"></a>때 toouse 오류 처리

오류 또는 예외를 throw 하는 중요 한 작업 인 때마다 중요 tooprevent hello 처리 및 toohandle hello 오류에서 runbook의 다음 작업 적절 하 게 큽니다. 이는 runbook에서 비즈니스 또는 서비스 운영 프로세스를 지원할 때 특히 중요합니다.

오류를 생성할 수 있는 각 활동에 대해 hello runbook 제작자 tooany 다른 활동을 가리키는 오류 링크를 추가할 수 있습니다.  hello 대상 활동 수 모든 형식의 코드 활동을 포함 하 여 다른 runbook을 호출 하는 cmdlet을 호출 수 등에입니다.

또한 hello 대상 활동 나가는 링크 있을 수도 있습니다. 이러한 링크는 일반 링크 또는 오류 링크일 수 있습니다. 즉, hello runbook 제작자 tooa 다시 정렬 하지 않고 복잡 한 오류 처리 논리를 구현할 수 작업 코딩 합니다. hello 좋습니다 toocreate 공통 된 기능을 사용 하 여 전용된 오류 처리 runbook 좋지만 필수는 아닙니다. 그럴 PowerShell 코드 활동에서 오류 처리 논리 hello만 옵션입니다.  

예를 들어 VM toostart를 시도 하는 runbook을 살펴보세요 고에 응용 프로그램을 설치 합니다. Hello VM 시작 되지 않는다면 올바르게 하는 경우 다음 두 가지 동작을 수행 합니다.

1. 이 문제에 대한 알림을 보냅니다.
2. 대신 새 VM을 자동으로 프로비전하는 다른 runbook을 시작합니다.

한 가지 해결 toohave tooan 활동 핸들 단계 1을 가리키는 오류 링크입니다. 예를 들어 hello를 연결할 수 있습니다 **Write-warning** hello 같은 2 단계에 대 한 cmdlet tooan 활동 **시작 AzureRmAutomationRunbook** cmdlet.

별도 오류 처리 runbook 및 다음 hello 지침 이전 제안으로 이러한 두 활동을 배치 하 여 많은 runbook에서 사용 하기 위해이 문제를 일반화할 수 있습니다. 이 오류 처리 runbook을 호출 하기 전에 hello 원래 runbook의 hello 데이터에서 사용자 지정 메시지를 생성 하 고 매개 변수 toohello 오류 처리 runbook로 전달 합니다 수 있습니다.

## <a name="how-toouse-error-handling"></a>어떻게 toouse 오류 처리

각 활동에는 예외를 종료되지 않는 오류로 전환하는 구성 설정이 있습니다. 이 설정은 기본적으로 사용하지 않도록 설정됩니다. Toohandle 오류의 하려는 모든 작업에 대해이 설정을 사용 하는 것이 좋습니다.  

이 구성의 기능을 사용 하 여 hello 활동의 오류를 모두 종료 및 종료 되지 않는 종료 되지 않는 오류로 처리 하 고 오류 링크도 처리할 수를 보장 됩니다.  

이 설정의 구성 후 hello 오류를 처리 하는 활동을 만듭니다. 작업에서 오류를 생성 하는 경우 다음 링크를 따르면 송신 오류 hello 및 hello 작업은 일반 출력도 생성 하는 경우에 hello 일반 링크로 폴링 되지 않는 합니다.<br><br> ![Automation runbook 오류 링크 예제](media/automation-runbook-graphical-error-handling/error-link-example.png)

다음 예제는 hello, runbook 가상 컴퓨터의 hello 컴퓨터 이름을 포함 하는 변수를 검색 합니다. 다음 활동 hello와 toostart hello 가상 컴퓨터를 시도합니다.<br><br> ![Automation runbook 오류 처리 예제](media/automation-runbook-graphical-error-handling/runbook-example-error-handling.png)<br><br>      

hello **Get-automationvariable** 활동 및 **시작 AzureRmVm** 구성된 tooconvert 예외 tooerrors 됩니다.  변수 또는 시작 hello 시키는 중 문제가 hello VM을 경우 오류가 생성 됩니다.<br><br> ![Automation runbook 오류 처리 활동 설정](media/automation-runbook-graphical-error-handling/activity-blade-convertexception-option.png)

이러한 활동 tooa 단일에서 흐름 오류 링크 **오류 관리** 활동 (코드 활동). 이 활동은 hello를 사용 하는 간단한 PowerShell 식으로 구성 되어 *Throw* 함께 사용 하 여 처리 하는 키워드 toostop *$Error.Exception.Message* hello를 설명 하는 tooget hello 메시지 현재 예외입니다.<br><br> ![Automation runbook 오류 처리 코드 예제](media/automation-runbook-graphical-error-handling/runbook-example-error-handling-code.png)


## <a name="next-steps"></a>다음 단계

* 그래픽 runbook에서 링크 형식 및 링크에 대해 자세히 toolearn 참조 [Azure 자동화의 그래픽 제작](automation-graphical-authoring-intro.md#links-and-workflow)합니다.

* toolearn toomonitor runbook 작업 및 기타 기술 정보가 참조 하는 방법 runbook 실행에 대 한 자세한 [runbook 작업을 추적할](automation-runbook-execution.md)합니다.
