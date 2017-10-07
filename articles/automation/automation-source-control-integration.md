---
title: "Azure 자동화에서 제어 통합 aaaSource | Microsoft Docs"
description: "이 문서에서는 Azure 자동화에서 GitHub를 사용하는 원본 제어 통합을 설명합니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 224d7375-9887-44dd-b137-06ffe396a4b4
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/21/2016
ms.author: magoedte;sngun
ms.openlocfilehash: 6ceee1de8065fafe85a13bbd7f585e74dbc96b47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="source-control-integration-in-azure-automation"></a>Azure 자동화에서 원본 제어 통합
소스 제어 통합 tooassociate runbook을 자동화 계정 tooa GitHub 소스 제어 리포지토리에 있습니다. 소스 제어 tooeasily을 사용 하면 팀 공동 작업, 변경 내용을 추적 및 runbook tooearlier 버전 롤백합니다. 예를 들어 소스 제어 있습니다 toosync 다른 소스 제어에서 분기 tooyour 개발, 테스트 또는 프로덕션 자동화 계정이 수, 자동화 개발 환경 tooyour 프로덕션에서 테스트 된 코드를 쉽게 toopromote 만들기 계정입니다.

소스 제어를 Azure 자동화 toosource 컨트롤에서 toopush 코드를 허용 하거나 소스 제어 tooAzure 자동화에서에서 runbook을 가져옵니다. 이 문서에서는 Azure 자동화 환경에서 소스를 tooset 제어 하는 방법을 설명 합니다. Azure 자동화 tooaccess GitHub 리포지토리를 구성 하 여 시작 하 고 수행할 수 있는 다른 작업을 안내 합니다 소스 제어 통합을 사용 하 여 합니다. 

> [!NOTE]
> 원본 제어는 [PowerShell 워크플로 Runbook](automation-runbook-types.md#powershell-workflow-runbooks) 뿐만 아니라 [PowerShell Runbook](automation-runbook-types.md#powershell-runbooks)의 끌어오기 및 밀어넣기를 지원합니다. [그래픽 Runbook](automation-runbook-types.md#graphical-runbooks)은 아직 지원되지 않습니다.<br><br>
> 
> 

자동화 계정에 대 한 두 가지 간단한 단계만 거치면 필요한 tooconfigure 소스 제어 및 하나만 GitHub 계정이 이미 있는 경우. 아래에 이 계정과 키의 예제가 나와 있습니다.

## <a name="step-1--create-a-github-repository"></a>1단계 - GitHub 리포지토리 만들기
이미 있는 경우 GitHub 계정 및 원하는 리포지토리 toolink tooAzure 자동화, 다음 로그인 tooyour 기존 계정 하 고 아래 2 단계에서 시작 합니다. 그렇지 않은 경우 너무 이동[GitHub](https://github.com/), 새 계정을 등록 하 고 [새 리포지토리를 만들](https://help.github.com/articles/create-a-repo/)합니다.

## <a name="step-2--set-up-source-control-in-azure-automation"></a>2단계 - Azure 자동화에서 원본 제어 설정
1. Hello Azure 포털의에서 자동화 계정 블레이드에서 hello에서 클릭 **소스 제어 설정 합니다.** 
   
    ![원본 제어 설정](media/automation-source-control-integration/automation_01_SetUpSourceControl.png)
2. hello **소스 제어** 블레이드에서 열립니다 GitHub 계정 세부 정보를 구성할 수 있습니다. 다음은 매개 변수 tooconfigure hello 목록이입니다.  
   
   | **매개 변수** | **설명** |
   |:--- |:--- |
   | 원본 선택 |Hello 원본을 선택 합니다. 현재는 **GitHub** 만 지원됩니다. |
   | 권한 부여 |Hello 클릭 **Authorize** 단추 toogrant Azure 자동화 액세스 tooyour GitHub 리포지토리 합니다. 이미 tooyour 다른 창에서 GitHub 계정이 로그인 하 고 다음 hello 해당 계정의 자격 증명이 사용 됩니다. 부여 된 hello 블레이드 프로그램 GitHub 사용자 이름에 표시 됩니다 **권한 부여 속성**합니다. |
   | 리포지토리 선택 |사용 가능한 저장소의 hello 목록에서 GitHub 리포지토리를 선택 합니다. |
   | 분기 선택 |Hello 목록을 사용할 수 있는 분기에서 분기를 선택 합니다. Hello만 **마스터** 분기는 분기를 만들지 않은 경우 표시 됩니다. |
   | Runbook 폴더 경로 |hello runbook 폴더 경로의 hello GitHub 리포지토리에 있는 toopush 하거나 코드를 끌어오도록 hello 경로 지정 합니다. Hello 형식으로 입력 해야 **/foldername/subfoldername**합니다. Hello runbook 폴더 경로의 runbook만 동기화 된 tooyour 자동화 계정이 됩니다. Hello runbook 폴더 경로의 hello 하위 폴더의 Runbook은 **하지** 동기화 할 수 있습니다. 사용 하 여  **/**  toosync hello 저장소에서 runbook을 hello 모든 합니다. |
3. 예를 들어 **RootFolder**라는 폴더를 포함하는 **PowerShellScripts**라는 리포지토리가 있는 경우 이는 **SubFolder**라는 폴더를 포함합니다. 각 폴더 수준 문자열 toosync 다음 hello를 사용할 수 있습니다.
   
   1. runbook toosync **리포지토리**, runbook 폴더 경로*/*
   2. runbook toosync **RootFolder**, runbook 폴더 경로가 */RootFolder*
   3. runbook toosync **하위 폴더**, runbook 폴더 경로가 */RootFolder/하위 폴더*합니다.
4. Hello에 표시 하는 hello 매개 변수를 구성한 후 **소스 제어 설정 블레이드에서 합니다.**  
   
    ![블레이드 구성](media/automation-source-control-integration/automation_02_SourceControlConfigure.png)
5. 확인을 클릭하면 원본 제어 통합은 자동화 계정에 대해 구성되고 GitHub 정보로 업데이트되어야 합니다. 클릭할 수 있습니다이 부분 tooview에 소스 제어의 모든 동기화 작업 기록 합니다.  
   
    ![리포지토리 값](media/automation-source-control-integration/automation_03_RepoValues.png)
6. 소스 제어를 설정한 후 hello 다음 자동화 리소스를 만들 것인지 자동화 계정에서:  
   두 개의 [변수 자산](automation-variables.md)이 만들어집니다.  
   
   * hello 변수 **Microsoft.Azure.Automation.SourceControl.Connection** 아래와 같이 hello 연결 문자열의 hello 값을 포함 합니다.  
     
     | **매개 변수** | **값** |
     |:--- |:--- |
     | 이름 |Microsoft.Azure.Automation.SourceControl.Connection |
     | 형식 |문자열 |
     | 값 |{"Branch":\<*분기 이름*>,"RunbookFolderPath":\<*Runbook 폴더 경로*>,"ProviderType":\<*GitHub에 대한 값 1을 가짐*>,"Repository":\<*리포지토리 이름*>,"Username":\<*GitHub 사용자 이름*>} |

    * hello 변수 **Microsoft.Azure.Automation.SourceControl.OAuthToken**, 프로그램 OAuthToken의 hello 안전한 암호화 된 값을 포함 합니다.  

    |**매개 변수**            |**값** |
    |:---|:---|
    | 이름  | Microsoft.Azure.Automation.SourceControl.OAuthToken |
    | 형식 | 알수 없음(암호화됨) |
    | 값 | <*암호화된 OAuthToken*> |  

    ![variables](media/automation-source-control-integration/automation_04_Variables.png)  

    * **자동화 소스 제어** 권한이 부여 된 응용 프로그램 tooyour GitHub 계정으로 추가 됩니다. tooview hello 응용 프로그램: GitHub 홈 페이지에서 이동 tooyour **프로필** > **설정** > **응용 프로그램**합니다. Azure 자동화 toosync GitHub 리포지토리 tooan 자동화 계정을 허용 하는이 응용 프로그램입니다.  

    ![Git 응용 프로그램](media/automation-source-control-integration/automation_05_GitApplication.png)


## <a name="using-source-control-in-automation"></a>자동화에서 원본 제어 사용
### <a name="check-in-a-runbook-from-azure-automation-toosource-control"></a>체크 인에 runbook이 Azure 자동화 toosource 컨트롤
Runbook 체크 인 수 toopush hello 변경을 내용이 tooa runbook Azure 자동화에서 소스 제어 리포지토리에 있습니다. 다음 toocheck의 hello 단계 runbook은.

1. 자동화 계정에서 [새 텍스트 Runbook 만들기](automation-first-runbook-textual.md) 또는 [기존 텍스트 Runbook 편집](automation-edit-textual-runbook.md)을 수행합니다. 이 runbook은 PowerShell 워크플로 또는 PowerShell 스크립트 runbook일 수 있습니다.  
2. Runbook을 편집한 후 저장 하 고 클릭 **인** hello에서 **편집** 블레이드입니다.  
   
    ![체크 인 단추](media/automation-source-control-integration/automation_06_CheckinButton.png)

     > [!NOTE] 
     > Azure 자동화에서 체크 인 현재 소스 제어에 있는 hello 코드를 덮어쓰게 됩니다. hello toocheck에 해당 하는 명령줄 명령 Git는 **git 추가 + git 커밋 + git 푸시**  

1. 클릭할 때 **인**, yes toocontinue 나타나면 확인 메시지가 표시 됩니다.  
   
    ![체크 인 메시지](media/automation-source-control-integration/automation_07_CheckinMessage.png)
2. 체크 인 시작 소스 제어 runbook hello: **동기화 MicrosoftAzureAutomationAccountToGitHubV1**합니다. 이 runbook tooGitHub 연결 하 고 Azure 자동화 tooyour 저장소에서 변경 내용을 푸시합니다. tooview hello 체크 인에 작업 기록, toohello 돌아가서 **소스 제어 통합** 탭을 tooopen hello 리포지토리 동기화 블레이드를 클릭 합니다. 이 블레이드는 모든 원본 제어 작업을 표시합니다.  Tooview 고 tooview hello 세부 정보 클릭 hello 작업을 선택 합니다.  
   
    ![체크 인 Runbook](media/automation-source-control-integration/automation_08_CheckinRunbook.png)
   
   > [!NOTE]
   > 원본 제어 Runbook은 보거나 편집할 수 없는 특별한 자동화 Runbook입니다. Runbook 목록에 표시되지 않지만 작업 목록에서 동기화 작업을 확인할 수 있습니다.
   > 
   > 
3. hello 이름은 수정 하는 hello runbook의 입력된 매개 변수 toohello 인 runbook으로 전송 됩니다. 할 수 있습니다 [hello 작업 세부 사항을 보는](automation-runbook-execution.md#viewing-job-status-from-the-azure-portal) 에서 runbook을 확장 하 여 **리포지토리 동기화** 블레이드입니다.  
   
    ![체크 인 입력](media/automation-source-control-integration/automation_09_CheckinInput.png)
4. Hello 작업 완료 tooview hello 변경 되 면 GitHub 리포지토리를 새로 고칩니다.  커밋 메시지를 사용 하 여 저장소에 커밋 있어야: **Updated *Runbook 이름* Azure 자동화에서 합니다.**  

### <a name="sync-runbooks-from-source-control-tooazure-automation"></a>소스 제어 tooAzure 자동화에서에서 runbook 동기화
hello 동기화 단추 hello 리포지토리 동기화 블레이드를 toopull을 사용 하면 프로그램 리포지토리 tooyour 자동화 계정의 hello runbook 폴더 경로의 runbook hello 모든 합니다. hello 같은 리포지토리 수 자동화 계정 하나 보다 동기화 된 toomore 합니다. Runbook hello 단계 toosync는 다음과 같습니다.

1. 자동화 계정 소스 제어를 설정 하는 위치 hello에서 hello 엽니다 **소스 제어를 통합/리포지토리 동기화 블레이드** 클릭 **동기화** 다음 확인 메시지가 나타납니다 메시지를 클릭 하 여 **예** toocontinue 합니다.  
   
    ![동기화 단추](media/automation-source-control-integration/automation_10_SyncButtonwithMessage.png)
2. Hello runbook을 시작 하는 동기화: **동기화 MicrosoftAzureAutomationAccountFromGitHubV1**합니다. 이 runbook tooGitHub 연결 하 고 프로그램 리포지토리 tooAzure 자동화의에서 hello 변경 내용을 끌어옵니다. Hello에서 새 작업을 볼 수 있어야 **리포지토리 동기화** 블레이드가이 동작에 대 한 합니다. hello 동기화 작업에 대 한 세부 정보 tooview tooopen hello 작업 세부 정보 블레이드에서 클릭 합니다.  
   
    ![동기화 Runbook](media/automation-source-control-integration/automation_11_SyncRunbook.png)

    > [!NOTE] 
    > 소스 제어에서 동기화에 대 한 자동화 계정에 현재 존재 하는 hello runbook의 초안 버전을 hello 덮어씁니다 **모든** runbook에 현재 있는 소스 제어 합니다. 해당 하는 명령줄 명령 toosync는 Git hello **git 끌어오기**


## <a name="troubleshooting-source-control-problems"></a>원본 제어 문제 해결
체크 인 또는 동기화 작업에 오류가 있을 경우 hello 작업 상태를 일시 중단 해야 하 고 hello 작업 블레이드에서 hello 오류에 대 한 자세한 정보를 볼 수 있습니다.  hello **모든 로그** 부분 안내해 PowerShell 스트림을 해당 작업과 연결 된 모든 hello 합니다. Hello 세부 정보와 함께 필요한 toohelp 체크 인 또는 동기화와 문제 해결을 제공 합니다. 또한 설명 hello 동기화 하거나 runbook 검사 기능에 동안 발생 하는 작업 순서.  

![AllLogs 이미지](media/automation-source-control-integration/automation_13_AllLogs.png)

## <a name="disconnecting-source-control"></a>원본 제어 연결 끊기
GitHub 계정에서 toodisconnect hello 리포지토리 동기화 블레이드를 열고 클릭 **연결 끊기**합니다. 소스 제어 연결을 해제 하면 이전에 동기화 된 runbook 자동화 계정에는 그대로 있지만 hello 리포지토리 동기화 블레이드를 사용할 수 없습니다.  

  ![연결 끊기 단추](media/automation-source-control-integration/automation_12_Disconnect.png)

## <a name="next-steps"></a>다음 단계
소스 제어 통합에 대 한 자세한 내용은 hello 다음 리소스를 참조 하세요.  

* [Azure 자동화: Azure 자동화에서 원본 제어 통합](https://azure.microsoft.com/blog/azure-automation-source-control-13/)  
* [즐겨 찾는 원본 제어 시스템에 대한 투표](https://www.surveymonkey.com/r/?sm=2dVjdcrCPFdT0dFFI8nUdQ%3d%3d)  
* [Azure 자동화: Visual Studio Team Services를 사용하여 Runbook 원본 제어 통합](https://azure.microsoft.com/blog/azure-automation-integrating-runbook-source-control-using-visual-studio-online/)  

