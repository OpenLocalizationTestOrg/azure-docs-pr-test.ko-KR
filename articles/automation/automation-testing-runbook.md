---
title: "Azure 자동화에서 runbook aaaTesting | Microsoft Docs"
description: "Azure 자동화에서 runbook을 게시 하기 전에 예상 대로 작동 tooensure를 테스트할 수 있습니다.  이 문서에서는 설명 방법을 tootest runbook 해당 출력을 봅니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 7f7db785-52c0-4613-aa12-b02fd32a5182
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/12/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 8c531f702699d586f8215d4c171cb0ecf94732b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="testing-a-runbook-in-azure-automation"></a>Azure 자동화에서 Runbook 테스트
Runbook을 테스트할 때는 hello [초안 버전](automation-creating-importing-runbook.md#publishing-a-runbook) 실행 되며 수행 하는 모든 작업이 완료 됩니다. 작업 기록은 만들어지기는 하지만 hello [출력](automation-runbook-output-and-messages.md#output-stream) 및 [경고 및 오류](automation-runbook-output-and-messages.md#message-streams) 스트림을 표시 하는 hello 테스트 출력 창. 메시지 toohello [Verbose Stream](automation-runbook-output-and-messages.md#message-streams) 경우에 hello hello 출력 창에에서 표시 됩니다 [$VerbosePreference 변수](automation-runbook-output-and-messages.md#preference-variables) tooContinue 설정 됩니다.

Hello 초안 버전을 실행 하는 경우에 hello runbook 여전히 hello 워크플로 정상적으로 실행 하 고 hello 환경에서 리소스에 대 한 모든 작업을 수행 합니다. 이러한 이유로 프로덕션이 아닌 리소스에서만 Runbook을 테스트해야 합니다.

프로시저 tootest hello [runbook의 형식을](automation-runbook-types.md) hello 동일 하 고 테스트 hello 텍스트 편집기와 hello hello Azure 포털의에서 그래픽 편집기 사이 차이가 없습니다.  

## <a name="tootest-a-runbook-in-hello-azure-portal"></a>tootest hello Azure 포털에서 runbook
사용 하 여 작업 수 [runbook 형식](automation-runbook-types.md) hello Azure 포털의에서.

1. 어느 hello에 hello runbook의 초안 버전 열기 hello [텍스트 편집기](automation-edit-textual-runbook.md) 또는 [그래픽 편집기](automation-graphical-authoring-intro.md)합니다.
2. Hello 클릭 **테스트** 단추 tooopen hello 테스트 블레이드입니다.
3. Hello runbook에 매개 변수가 hello 테스트에 사용 되는 값 toobe를 제공할 수 있는 hello 왼쪽된 창에 나열 됩니다.
4. toorun hello 테스트 하려는 경우는 [Hybrid Runbook Worker](automation-hybrid-runbook-worker.md), 다음 변경 **실행 설정** 너무**Hybrid Worker** 및 hello 대상 그룹의 이름을 선택 hello 합니다.  그렇지 않으면 hello 기본값을 유지 **Azure** hello 클라우드에서 toorun hello 테스트 합니다.
5. Hello 클릭 **시작** 단추 toostart hello 테스트 합니다.
6. Hello runbook이 [PowerShell 워크플로](automation-runbook-types.md#powershell-workflow-runbooks) 또는 [그래픽](automation-runbook-types.md#graphical-runbooks), 다음 hello 출력 창 아래의 hello 단추를 사용 하 여 테스트 되는 일시 중단 하거나 중지할 수 있습니다. Hello runbook을 일시 중단 하는 경우 일시 중단 되기 전에 hello 현재 작업이 완료 합니다. Hello runbook이 일시 중단 되 면 중지 하거나 다시 시작할 수 있습니다.
7. Hello hello 출력 창에는 runbook에서 hello 출력을 검사 합니다.

## <a name="next-steps"></a>다음 단계
* toocreate 또는 가져오기 runbook 확인 하려면 어떻게 해야 toolearn [만들기 또는 Azure 자동화에서 runbook 가져오기](automation-creating-importing-runbook.md)
* 그래픽 작성에 대 한 더 toolearn 참조 [Azure 자동화의 그래픽 제작](automation-graphical-authoring-intro.md)
* PowerShell 워크플로 runbook 시작 tooget 참조 [내 첫 번째 PowerShell 워크플로 runbook](automation-first-runbook-textual.md)
* runboks tooreturn 상태 메시지 및 권장 되는 방법을 비롯 하 여 오류 구성에 대 한 더 toolearn 참조 [Runbook 출력 및 Azure 자동화에서 메시지](automation-runbook-output-and-messages.md)

