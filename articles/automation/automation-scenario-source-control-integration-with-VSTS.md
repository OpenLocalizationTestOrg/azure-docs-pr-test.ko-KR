---
title: "소스 제어 Visual Stuido Team Services와 Azure 자동화 aaaIntegrate | Microsoft Docs"
description: "Azure Automation 계정 및 Visual Stuido Team Services 소스 제어와의 통합 설정을 안내하는 시나리오입니다."
services: automation
documentationcenter: 
author: eamono
manager: 
editor: 
keywords: "azure powershell, VSTS, 소스 제어, Automation"
ms.assetid: a43b395a-e740-41a3-ae62-40eac9d0ec00
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.openlocfilehash: 8f6faa596a5ad1f8b72e820ca320b3e103d83579
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---automation-source-control-integration-with-visual-studio-team-services"></a>Azure Automation 시나리오 - Visual Studio Team Services와 Automation 소스 제어 통합

이 시나리오에서 toomanage Azure 자동화 runbook 또는 소스 제어에서 DSC 구성을 사용 하는 Visual Studio Team Services 프로젝트를 수 있습니다.
이 문서에서는 설명 방법을 toointegrate VSTS 각 체크 인에 대 한 연속 통합을 지에서 발생 하므로 Azure 자동화 환경입니다.

## <a name="getting-hello-scenario"></a>Hello 시나리오를 가져오기

이 시나리오 hello에서 직접 가져올 수 있는 두 개의 PowerShell runbook 이루어져 [Runbook 갤러리](automation-runbook-gallery.md) hello Azure 포털 또는 hello에서 다운로드 [PowerShell 갤러리](https://www.powershellgallery.com)합니다.

### <a name="runbooks"></a>Runbook

Runbook | 설명| 
--------|------------|
Sync-VSTS | 체크 인 작업이 완료되면 VSTS 소스 제어에서 runbook 또는 구성을 가져옵니다. 수동으로 실행 가져오기 되며 모든 runbook 또는 hello 자동화 계정에 구성을 게시 합니다.| 
Sync-VSTSGit | 체크 인 작업이 완료되면 Git 소스 제어의 VSTS에서 runbook 또는 구성을 가져옵니다. 수동으로 실행 가져오기 되며 모든 runbook 또는 hello 자동화 계정에 구성을 게시 합니다.|

### <a name="variables"></a>variables

변수 | 설명|
-----------|------------|
VSToken | 만들려는 hello VSTS 개인용 액세스 토큰을 포함 하는 변수 자산을 보호 합니다. VSTS 개인용 액세스 하는 toocreate 방법을 학습할 수 있는 hello에 토큰 [VSTS 인증 페이지](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview)합니다. 
## <a name="installing-and-configuring-this-scenario"></a>이 시나리오 설치 및 구성

만들기는 [개인용 액세스 토큰](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview) 저마다 자동화 계정으로 toosync hello runbook 또는 구성을 사용 합니다.

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPersonalToken.png) 

만들기는 [secure 변수의](automation-variables.md) 프로그램 자동화 계정 toohold hello 개인용 액세스 토큰 hello runbook tooVSTS 및 동기화 hello runbook 또는 구성이 hello 자동화 계정에 인증할 수 있도록 합니다. 이름을 VSToken으로 지정할 수 있습니다. 

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSTokenVariable.png)

Runbook 또는 hello 자동화 계정으로 구성 동기화 hello runbook을 가져옵니다. Hello를 사용할 수 있습니다 [VSTS 샘플 runbook](https://www.powershellgallery.com/packages/Sync-VSTS/1.0/DisplayScript) 또는 hello [Git 샘플 runbook과 VSTS] (https://www.powershellgallery.com/packages/Sync-VSTSGit/1.0/DisplayScript) VSTS 사용 여부에 따라 PowerShellGallery.com hello에서 원본 제어 또는 git VSTS tooyour 자동화 계정을 배포 합니다.

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPowerShellGallery.png)

이제 webhook을 만들 수 있도록 이 runbook을 [게시](automation-creating-importing-runbook.md#publishing-a-runbook)할 수 있습니다. 
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPublishRunbook.png)

만들기는 [webhook](automation-webhooks.md) 이 동기화 VSTS runbook 및 아래와 같이 hello 매개 변수를 입력 합니다. VSTS에서 서비스 후크에 대 한 필요 하므로 hello webhook url을 복사 하 고 있는지 확인 합니다. hello VSAccessTokenVariableName hello 이름 (VSToken)을 이전 toohold hello 개인용 액세스 토큰을 만든 hello 보안 변수입니다. 

VSTS (동기화 VSTS.ps1)와 통합 하면 매개 변수 뒤 hello를 소요 됩니다.
### <a name="sync-vsts-parameters"></a>Sync-VSTS 매개 변수

매개 변수 | 설명| 
--------|------------|
WebhookData | Hello VSTS 서비스 후크에서 보내는 hello 체크 인 정보를 포함 됩니다. 이 매개 변수는 비워 두어야 합니다.| 
ResourceGroup | Hello 자동화 계정에 있는 hello 리소스 그룹의 hello 이름입니다.|
AutomationAccountName | hello hello 자동화 계정의 이름입니다 VSTS와 동기화 됩니다.|
VSFolder | Hello runbook 및 구성이 있는 VSTS에서 hello 폴더의 이름입니다.|
VSAccount | Visual Studio Team Services 계정 hello의 hello 이름입니다.| 
VSAccessTokenVariableName | hello VSTS 개인용 액세스 토큰을 보유 하는 hello secure 변수의 (VSToken)의 hello 이름입니다.| 


![](media/automation-scenario-source-control-integration-with-VSTS/VSTSWebhook.png)

VSTS (동기화 VSTSGit.ps1) GIT와 함께 사용 하는 경우 매개 변수 뒤 hello를 걸립니다.

매개 변수 | 설명|
--------|------------|
WebhookData | Hello VSTS 서비스 후크에서 보내는 hello 체크 인 정보를 포함 됩니다. 이 매개 변수는 비워 두어야 합니다.| ResourceGroup | 이 hello는 hello 자동화 계정에 있는 hello 리소스 그룹의 이름입니다.|
AutomationAccountName | hello hello 자동화 계정의 이름입니다 VSTS와 동기화 됩니다.|
VSAccount | Visual Studio Team Services 계정 hello의 hello 이름입니다.|
VSProject | hello runbook 및 구성이 있는 VSTS에서 hello 프로젝트의 hello 이름입니다.|
GitRepo | hello Git 리포지토리의 hello 이름입니다.|
GitBranch | hello 이름 hello VSTS Git 리포지토리의 분기입니다.|
폴더 | VSTS Git 분기에서 hello 폴더의 hello 이름입니다.|
VSAccessTokenVariableName | hello VSTS 개인용 액세스 토큰을 보유 하는 hello secure 변수의 (VSToken)의 hello 이름입니다.|

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSGitWebhook.png)

VSTS에서 코드 체크 인에이 webhook을 트리거하는 체크 인 toohello 폴더에 대 한 서비스 후크를 만듭니다. 새 구독을 만들 때와 hello 서비스 toointegrate로 Web Hook를 선택 합니다. [VSTS 서비스 후크 설명서](https://www.visualstudio.com/en-us/docs/marketplace/integrate/service-hooks/get-started)에서 서비스 후크에 대해 자세히 알아볼 수 있습니다.
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSServiceHook.png)

이제 수 toodo runbook 및 VSTS 구성을의 체크 인 될 하 고 자동으로 이러한 사항이 동기화 해야 자동화 계정으로 했습니다.

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSSyncRunbookOutput.png)

이 runbook을 VSTS에서 트리거된 하지 않고 수동으로 실행 하는 경우 hello webhookdata 매개 변수를 비워 둘 수 있습니다 및 지정 된 hello VSTS 폴더에서 전체 동기화를 수행 합니다.

VSTS에서 hello 서비스 후크 제거 toouninstall hello 시나리오를 원한다 면 hello runbook 및 hello VSToken 변수를 삭제 합니다.
