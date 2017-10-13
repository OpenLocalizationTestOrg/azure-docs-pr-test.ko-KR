---
title: "Visual Studio Team Services 소스 제어에 Azure Automation 통합 | Microsoft Docs"
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
ms.openlocfilehash: 01f9c01c9e04e02dbb548b68cf99684ba6ddd57e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario---automation-source-control-integration-with-visual-studio-team-services"></a>Azure Automation 시나리오 - Visual Studio Team Services와 Automation 소스 제어 통합

이 시나리오에서는 소스 제어에서 Azure Automation 또는 DSC 구성을 관리하는 데 Visual Studio Team Services 프로젝트를 사용하고 있다고 가정합니다.
이 문서에서는 각 체크 인에 대해 연속 통합이 발생할 수 있도록 Azure Automation 환경에 VSTS를 통합하는 방법을 설명합니다.

## <a name="getting-the-scenario"></a>시나리오 가져오기

이 시나리오는 Azure 포털의 [Runbook 갤러리](automation-runbook-gallery.md)에서 직접 가져오거나 [PowerShell 갤러리](https://www.powershellgallery.com)에서 다운로드할 수 있는 2개의 PowerShell runbook으로 구성됩니다.

### <a name="runbooks"></a>Runbook

Runbook | 설명| 
--------|------------|
Sync-VSTS | 체크 인 작업이 완료되면 VSTS 소스 제어에서 runbook 또는 구성을 가져옵니다. 수동으로 실행하는 경우 모든 runbook 또는 구성을 Automation 계정으로 가져와 게시합니다.| 
Sync-VSTSGit | 체크 인 작업이 완료되면 Git 소스 제어의 VSTS에서 runbook 또는 구성을 가져옵니다. 수동으로 실행하는 경우 모든 runbook 또는 구성을 Automation 계정으로 가져와 게시합니다.|

### <a name="variables"></a>변수

변수 | 설명|
-----------|------------|
VSToken | VSTS 개인 액세스 토큰이 포함된 변수 자산을 만들어 보호합니다. [VSTS 인증 페이지](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview)에서 VSTS 개인 액세스 토큰을 만드는 방법을 알아볼 수 있습니다. 
## <a name="installing-and-configuring-this-scenario"></a>이 시나리오 설치 및 구성

runbook 또는 구성을 Automation 계정에 동기화하는 데 사용할 [개인 액세스 토큰](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview)을 VSTS에 만듭니다.

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPersonalToken.png) 

VSTS에서 runbook을 인증하고 runbook 및 구성을 Automation 계정에 동기화할 수 있도록 Automation 계정에 개인 액세스 토큰을 저장할 [보안 변수](automation-variables.md)를 만듭니다. 이름을 VSToken으로 지정할 수 있습니다. 

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSTokenVariable.png)

runbook 또는 구성을 Automation 계정에 동기화하는 runbook을 가져옵니다. VSTS 소스 제어를 사용하는지 또는 Git이 있는 VSTS를 사용하여 Automation 계정에 배포하는지에 따라 [VSTS 샘플 runbook](https://www.powershellgallery.com/packages/Sync-VSTS/1.0/DisplayScript) 또는 PowerShellGallery.com(https://www.powershellgallery.com/packages/Sync-VSTSGit/1.0/DisplayScript)의 [Git이 있는 VSTS 샘플 runbook]을 사용할 수 있습니다.

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPowerShellGallery.png)

이제 webhook을 만들 수 있도록 이 runbook을 [게시](automation-creating-importing-runbook.md#publishing-a-runbook)할 수 있습니다. 
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPublishRunbook.png)

이 Sync-VSTS runbook에 대해 [webhook](automation-webhooks.md)을 만들고 아래와 같이 매개 변수를 입력합니다. VSTS의 서비스 후크에 필요하므로 webhook URL을 복사해야 합니다. VSAccessTokenVariableName은 개인 액세스 토큰을 저장하기 위해 앞에서 만든 보안 변수의 이름(VSToken)입니다. 

VSTS(Sync-VSTS.ps1)와 통합하면 다음과 같은 매개 변수가 사용됩니다.
### <a name="sync-vsts-parameters"></a>Sync-VSTS 매개 변수

매개 변수 | 설명| 
--------|------------|
WebhookData | VSTS 서비스 후크에서 전송되는 체크 인 정보가 포함됩니다. 이 매개 변수는 비워 두어야 합니다.| 
ResourceGroup | Automation 계정이 있는 리소스 그룹의 이름입니다.|
AutomationAccountName | VSTS와 동기화될 Automation 계정의 이름입니다.|
VSFolder | runbook 및 구성이 있는 VSTS의 폴더 이름입니다.|
VSAccount | Visual Studio Team Services 계정의 이름입니다.| 
VSAccessTokenVariableName | VSTS 개인 액세스 토큰을 보유하는 보안 변수(VSToken)의 이름입니다.| 


![](media/automation-scenario-source-control-integration-with-VSTS/VSTSWebhook.png)

GIT이 있는 VSTS(Sync-VSTSGit.ps1)를 사용하는 경우 다음 매개 변수가 사용됩니다.

매개 변수 | 설명|
--------|------------|
WebhookData | VSTS 서비스 후크에서 전송되는 체크 인 정보가 포함됩니다. 이 매개 변수는 비워 두어야 합니다.| ResourceGroup | Automation 계정이 있는 리소스 그룹의 이름입니다.|
AutomationAccountName | VSTS와 동기화될 Automation 계정의 이름입니다.|
VSAccount | Visual Studio Team Services 계정의 이름입니다.|
VSProject | runbook 및 구성이 있는 VSTS의 프로젝트 이름입니다.|
GitRepo | Git 리포지토리의 이름입니다.|
GitBranch | VSTS Git 리포지토리의 분기 이름입니다.|
폴더 | VSTS Git 분기에 있는 폴더의 이름입니다.|
VSAccessTokenVariableName | VSTS 개인 액세스 토큰을 보유하는 보안 변수(VSToken)의 이름입니다.|

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSGitWebhook.png)

코드 체크 인 시, 이 webhook을 트리거하는 폴더로의 체크 인을 위해 VSTS에 서비스 후크를 만듭니다. 새 구독을 만들 때 통합할 서비스로 webhook를 선택합니다. [VSTS 서비스 후크 설명서](https://www.visualstudio.com/en-us/docs/marketplace/integrate/service-hooks/get-started)에서 서비스 후크에 대해 자세히 알아볼 수 있습니다.
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSServiceHook.png)

이제 VSTS에 대한 runbook 및 구성의 모든 체크 인을 수행하고 이러한 항목을 Automation 계정에 자동으로 동기화할 수 있습니다.

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSSyncRunbookOutput.png)

VSTS에 의해 트리거되지 않고 수동으로 이 runbook을 실행하는 경우 webhookdata 매개 변수를 비워 둘 수 있습니다. 그러면 지정된 VSTS 폴더에서 전체 동기화가 수행됩니다.

이 시나리오를 제거하려면 VSTS에서 서비스 후크를 제거하고 runbook 및 VSToken 변수를 삭제합니다.
