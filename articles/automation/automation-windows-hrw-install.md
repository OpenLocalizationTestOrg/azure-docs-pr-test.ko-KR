---
title: Azure Automation Windows Hybrid Runbook Worker | Microsoft Docs
description: "이 문서에서는 로컬 데이터 센터 또는 클라우드 환경의 Windows 기반 컴퓨터에서 Runbook을 실행할 수 있도록 해주는 Azure Automation Hybrid Runbook Worker를 설치하는 방법에 대한 정보를 제공합니다."
services: automation
documentationcenter: 
author: georgewallace
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/07/2017
ms.author: magoedte
ms.openlocfilehash: 71c98a7e17472ae0aa7646b9e7fc745363546211
ms.sourcegitcommit: 0e4491b7fdd9ca4408d5f2d41be42a09164db775
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="how-to-deploy-a-windows-hybrid-runbook-worker"></a>Windows Hybrid Runbook Worker를 배포하는 방법

Azure Automation의 Runbook은 Azure 클라우드에서 실행되므로 다른 클라우드 또는 온-프레미스 환경의 리소스에 액세스할 수 없습니다.  Azure Automation의 Hybrid Runbook Worker 기능을 사용하면 컴퓨터에 대해 직접 그리고 외부에서 환경의 리소스에 대해 Runbook을 실행하여 로컬 리소스를 관리할 수 있습니다. Runbook은 Azure Automation에 저장 및 관리된 후 하나 이상의 지정된 컴퓨터에 전달됩니다.  

이 기능은 다음 이미지에 나와 있습니다.<br>

![Hybrid Runbook Worker 개요](media/automation-offering-get-started/automation-infradiagram-networkcomms.png)

Hybrid Runbook Worker 역할의 기술적 개요 및 배포 고려 사항은 [Automation 아키텍처 개요](automation-offering-get-started.md#automation-architecture-overview)를 참조하세요.

## <a name="hybrid-runbook-worker-groups"></a>Hybrid Runbook Worker 그룹

각 Hybrid Runbook Worker는 에이전트를 설치할 때 지정한 Hybrid Runbook Worker 그룹의 구성원입니다.  그룹은 단일 에이전트를 포함할 수 있지만 고가용성을 위해 그룹에 여러 에이전트를 설치할 수 있습니다.

Hybrid Runbook Worker에서 Runbook을 시작할 경우 이를 실행할 그룹을 지정합니다.  그룹의 구성원에 따라 요청을 처리할 작업자가 결정됩니다.  특정 작업자를 지정할 수 없습니다.

## <a name="installing-the-windows-hybrid-runbook-worker"></a>Windows Hybrid Runbook Worker 설치 

Windows Hybrid Runbook Worker를 설치 및 구성하려면 2가지 방법을 사용할 수 있습니다.  권장되는 방법은 Automation Runbook을 사용하여 Windows 컴퓨터를 구성하는 데 필요한 프로세스를 완전히 자동화하는 것입니다.  두 번째 방법은 단계별 절차에 따라 역할을 수동으로 설치하고 구성하는 것입니다.  

> [!NOTE]
> DSC(필요한 상태 구성)로 Hybrid Runbook Worker 역할을 지원하는 서버의 구성을 관리하려면 이들을 DSC 노드로 추가해야 합니다.  DSC를 통한 관리를 위한 온보드에 대한 정보는 [Azure Automation DSC를 통한 관리를 위한 컴퓨터 온보드](automation-dsc-onboarding.md)를 참조하세요.        
[관리 솔루션 업데이트](../operations-management-suite/oms-solution-update-management.md)를 사용하도록 설정하면 이 솔루션에 포함된 Runbook을 지원하기 위해 OMS 작업 영역에 연결된 모든 Windows 컴퓨터가 자동으로 Hybrid Runbook Worker로 구성됩니다.  그러나 Automation 계정에서 이미 정의한 모든 Hybrid Worker 그룹에 등록되지 않았습니다.  솔루션과 Hybrid Runbook Worker 그룹 멤버 자격에 동일한 계정을 사용하는 한 Automation Runbook을 지원하기 위해 Automation 계정의 Hybrid Runbook Worker 그룹에 컴퓨터를 추가할 수 있습니다.  이 기능은 Hybrid Runbook Worker의 7.2.12024.0 버전에 추가되었습니다.  

Hybrid Runbook Worker 배포를 시작하기 전에 [하드웨어 및 소프트웨어 요구 사항](automation-offering-get-started.md#hybrid-runbook-worker) 및 [네트워크 준비를 위한 정보](automation-offering-get-started.md#network-planning)에 대한 다음 정보를 검토합니다.  Runbook Worker를 성공적으로 배포한 후에는 [Hybrid Runbook Worker에서 Runbook 실행](automation-hrw-run-runbooks.md)을 검토하여 온-프레미스 데이터 센터 또는 다른 클라우드 환경의 프로세스를 자동화하도록 Runbook을 구성하는 방법을 알아봅니다.  
 
### <a name="automated-deployment"></a>자동화된 배포

다음 단계에 따라 Windows Hybrid Worker 역할의 설치와 구성을 자동화합니다.  

1. Hybrid Runbook Worker 역할을 실행하는 컴퓨터에서 직접 또는 사용자 환경의 다른 컴퓨터에서 [PowerShell 갤러리](https://www.powershellgallery.com/packages/New-OnPremiseHybridWorker/1.0/DisplayScript)의 *새로 OnPremiseHybridWorker.ps1* 스크립트를 다운로드한 후 작업자에 복사합니다.  

    *New-OnPremiseHybridWorker.ps1* 스크립트에는 실행 중 다음 매개 변수가 필요합니다.

  * *AutomationAccountName*(필수) - Automation 계정의 이름  
  * *ResourceGroupName*(필수) - Automation 계정과 연결된 리소스 그룹의 이름  
  * *HybridGroupName*(필수) - 이 시나리오를 지원하는 Runbook에 대한 대상으로 지정할 Hybrid Runbook Worker 그룹의 이름 
  *  *SubscriptionID*(필수) - Automation 계정이 있는 Azure 구독 ID
  *  *WorkspaceName*(선택) - OMS 작업 영역 이름  OMS 작업 영역이 없는 경우 스크립트에서 하나를 만들어 구성합니다.  

     > [!NOTE]
     > 현재 OMS와 통합되도록 지원되는 Automation 영역은 **오스트레일리아 남동부**, **미국 동부 2**, **동남 아시아** 및 **서유럽**뿐입니다.  이러한 영역 중 하나에 Automation 계정에 없는 경우 스크립트에서 OMS 작업 영역을 만들지만 연결할 수 없다고 경고합니다.
     >
2. 컴퓨터에서 관리자 모드의 **시작** 화면에서 **Windows PowerShell**을 시작합니다.  
3. PowerShell 명령줄 셸에서 다운로드한 스크립트가 포함된 폴더로 이동한 후 *-AutomationAccountName*, *-ResourceGroupName*, *-HybridGroupName*, *-SubscriptionId* 및 *-WorkspaceName* 매개 변수 값을 변경하여 실행합니다.

     > [!NOTE] 
     > 스크립트를 실행한 후에 Azure 인증을 묻는 메시지가 나타납니다.  구독 관리자 역할의 멤버이자 구독의 공동 관리자인 계정으로 **로그인해야** 합니다.  
     >  
    
        .\New-OnPremiseHybridWorker.ps1 -AutomationAccountName <NameofAutomationAccount> `
        -ResourceGroupName <NameofOResourceGroup> -HybridGroupName <NameofHRWGroup> `
        -SubscriptionId <AzureSubscriptionId> -WorkspaceName <NameOfOMSWorkspace>

4. **NuGet**을 설치할지 묻는 메시지가 표시되고 Azure 자격 증명으로 인증을 받도록 요구됩니다.<br><br> ![New-OnPremiseHybridWorker 스크립트 실행](media/automation-hybrid-runbook-worker/new-onpremisehybridworker-scriptoutput.png)

5. 스크립트가 완료되면 Hybrid Worker 그룹 블레이드에 새 그룹 및 멤버 수가 표시되고, 기존 그룹이 있으면 해당 멤버 수가 증가됩니다.  **Hybrid Worker 그룹** 블레이드의 목록에서 그룹을 선택하고 **Hybrid Worker** 타일을 선택합니다.  **Hybrid Worker** 블레이드에서 나열된 그룹의 각 멤버를 확인합니다.  

### <a name="manual-deployment"></a>수동 배포 

Automation 환경에 대해 처음 두 단계를 한 번 수행한 후 각 Worker 컴퓨터에 대해 나머지 단계를 반복합니다.

#### <a name="1-create-operations-management-suite-workspace"></a>1. Operations Management Suite 작업 영역 만들기

Operations Management Suite 작업 영역이 아직 없는 경우 [작업 영역 관리](../log-analytics/log-analytics-manage-access.md)의 지침에 따라 작업 영역을 만듭니다. 이미 있는 경우에는 기존 작업 영역을 사용할 수 있습니다.

#### <a name="2-add-automation-solution-to-operations-management-suite-workspace"></a>2. Operations Management Suite 작업 영역에 Automation 솔루션 추가

솔루션은 Operations Management Suite에 기능을 추가합니다.  Automation 솔루션은 Hybrid Runbook Worker에 대한 지원을 포함하여 Azure Automation을 위한 기능을 추가합니다.  작업 영역에 솔루션을 추가할 때 다음 단계에서 설치할 에이전트 컴퓨터로 Worker 구성 요소를 자동으로 푸시다운합니다.

[솔루션 갤러리를 사용하여 솔루션을 추가하려면](../log-analytics/log-analytics-add-solutions.md) 의 지침에 따라 Operations Management Suite 작업 영역에 **Automation** 솔루션을 추가합니다.

#### <a name="3-install-the-microsoft-monitoring-agent"></a>3. Microsoft Monitoring Agent 설치

Microsoft 모니터링 에이전트는 컴퓨터를 Operations Management Suite에 연결합니다.  온-프레미스 컴퓨터에 에이전트를 설치하고 작업 영역에 연결하면 Hybrid Runbook Worker에 필요한 구성 요소가 자동으로 다운로드됩니다.

[Log Analytics에 Windows 컴퓨터 연결](../log-analytics/log-analytics-windows-agent.md)의 지침에 따라 온-프레미스 컴퓨터에 에이전트를 설치합니다.  이 과정을 여러 컴퓨터에 반복하여 사용자의 환경에 여러 작업자를 추가합니다.

에이전트가 Operations Management Suite에 연결되면 Operations Management Suite **설정** 창의 **Connected Sources**(연결된 원본) 탭에 나열됩니다.  에이전트에서 Automation 솔루션 다운로드를 완료했는지 확인하려면 C:\Program Files\Microsoft Monitoring Agent\Agent에 **AzureAutomationFiles** 폴더가 있는지 확인합니다.  Hybrid Runbook Worker의 버전을 확인하려면 C:\Program Files\Microsoft Monitoring Agent\Agent\AzureAutomation\으로 이동하고 \\*version* 하위 폴더를 적어두세요.   

#### <a name="4-install-the-runbook-environment-and-connect-to-azure-automation"></a>4. Runbook 환경을 설치하고 Azure Automation에 연결

에이전트를 Operations Management Suite에 추가하면 Automation 솔루션이 **Add-HybridRunbookWorker** cmdlet을 포함하는 **HybridRegistration** PowerShell 모듈을 푸시다운합니다.  이 cmdlet을 사용하여 컴퓨터에 Runbook 환경을 설치하고 Azure Automation에 등록합니다.

관리자 모드에서 PowerShell 세션을 열고 다음 명령을 실행하여 모듈을 가져옵니다.

    cd "C:\Program Files\Microsoft Monitoring Agent\Agent\AzureAutomation\<version>\HybridRegistration"
    Import-Module HybridRegistration.psd1

그런 다음 아래 구문을 사용하여 **Add-HybridRunbookWorker** cmdlet을 실행합니다.

    Add-HybridRunbookWorker –GroupName <String> -EndPoint <Url> -Token <String>

Azure portal의 **키 관리** 블레이드에서 이 cmdlet에 필요한 정보를 가져올 수 있습니다.  Automation 계정의 **설정** 블레이드에서 **키** 옵션을 선택하여 이 블레이드를 엽니다.

![Hybrid Runbook Worker 개요](media/automation-hybrid-runbook-worker/elements-panel-keys.png)

* **GroupName**은 Hybrid Runbook Worker 그룹의 이름입니다. 이 그룹이 자동화 계정에 이미 있으면 현재 컴퓨터가 추가되고,  그렇지 않으면 이 그룹이 추가됩니다.
* **끝점**은 **키 관리** 블레이드의 **URL** 필드입니다.
* **Token**은 **키 관리** 블레이드의 **기본 액세스 키**입니다.  

설치에 대해 자세한 정보를 받으려면 **Add-HybridRunbookWorker**와 함께 **-Verbose** 스위치를 사용합니다.

#### <a name="5-install-powershell-modules"></a>5. PowerShell 모듈 설치

Runbook은 Azure Automation 환경에 설치된 모듈에 정의된 활동 및 cmdlet을 사용할 수 있습니다.  이러한 모듈은 온-프레미스 컴퓨터에 자동으로 배포되지 않으므로 수동으로 설치해야 합니다.  단, 기본적으로 설치되어 Azure Automation의 모든 Azure 서비스 및 활동에 사용되는 cmdlet에 대한 액세스를 제공하는 Azure 모듈은 예외입니다.

Hybrid Runbook Worker 기능의 주 목적은 로컬 리소스를 관리하는 것이므로 이러한 리소스를 지원하는 모듈을 설치해야 할 수 있습니다.  Windows PowerShell 모듈 설치에 대한 자세한 내용은 [모듈 설치](http://msdn.microsoft.com/library/dd878350.aspx) 를 참조하세요.  설치된 모듈은 Hybrid Worker가 자동으로 가져올 수 있도록 PSModulePath 환경 변수가 참조하는 위치에 있어야 합니다.  추가 정보는 [PSModulePath 설치 경로 수정](https://msdn.microsoft.com/library/dd878326%28v=vs.85%29.aspx)을 참조하세요. 

## <a name="troubleshooting"></a>문제 해결 

Hybrid Runbook Worker는 Automation 계정과 통신하여 작업자를 등록하고, Runbook 작업을 수신하고, 상태를 보고하는 Microsoft Monitoring Agent에 따라 달라집니다. 작업자 등록이 실패할 경우 가능한 오류 원인으로 몇 가지가 있습니다.  

1. Hybrid Worker가 프록시 또는 방화벽 뒤에 있습니다.  
    *.azure-automation.net에 대한 아웃바운드 액세스 권한이 컴퓨터의 443 포트에 있는지 확인합니다.  

2. 하이브리드 작업자가 실행되는 컴퓨터가 최소 하드웨어 [요구 사항](automation-offering-get-started.md#hybrid-runbook-worker)을 충족하지 않습니다.  
    Hybrid Runbook Worker가 실행되는 컴퓨터는 이 기능을 호스트하도록 지정하기 전에, 최소 하드웨어 요구 사항을 충족해야 합니다. 그렇지 않으면, 실행 중 Runbook에 의해 유발되는 다른 백그라운드 프로세스 및 경합의 리소스 사용률에 따라, 컴퓨터가 과도하게 사용되거나 Runbook 작업이 지연되거나 시간이 초과되는 원인이 될 수 있습니다.
   Hybrid Runbook Worker 기능을 실행하도록 지정된 컴퓨터가 최소 하드웨어 요구 사항을 충족하는지 확인합니다.  그렇다면, CPU 및 메모리 사용률을 모니터링하여 Hybrid Runbook Worker 프로세스와 Windows 사이에 어떠한 상관 관계가 있는지 확인합니다.  메모리 또는 CPU가 과도하게 사용된다면, 리소스 디스크 병목 현상에 대처하고 오류를 해결하기 위해 메모리를 증가시키거나 프로세서를 업그레이드 또는 추가해야 한다는 것을 나타냅니다. 아니면, 최소 요구 사항을 지원할 수 있는 다른 계산 리소스를 선택하고 필요한 워크로드에 증가가 필요하다는 것이 나타나면 규모를 확장합니다.
    
3. Microsoft Monitoring Agent 서비스가 실행되고 있지 않습니다.  
    Microsoft Monitoring Agent Windows 서비스가 실행되고 있지 않으면 Hybrid Runbook Worker가 Azure Automation과 통신할 수 없습니다.  PowerShell에서 `get-service healthservice` 명령을 입력하여 에이전트가 실행 중인지 확인하세요.  서비스가 중지된 경우 PowerShell에서 `start-service healthservice` 명령을 입력하여 서비스를 시작하세요.  

4. **Application and Services Logs\Operations Manager** 이벤트 로그에 이벤트 4502 및 **Microsoft.EnterpriseManagement.HealthService.AzureAutomation.HybridAgent**가 포함된 EventMessage와 함께 다음 설명이 보입니다. *<wsid>. oms.opinsights.azure.com 서비스에서 제공한 인증서가 Microsoft 서비스에 사용되는 인증 기관에서 발급한 것이 아닙니다. 네트워크 관리자에게 문의하여 TLS/SSL 통신을 가로채는 프록시를 실행하고 있는지 확인하세요. 문서 KB3126513에는 연결 문제에 대한 추가 문제 해결 정보가 들어 있습니다.*
    프록시 또는 네트워크 방화벽이 Microsoft Azure와의 통신을 차단하는 것일 수 있습니다.  *.azure-automation.net에 대한 아웃바운드 액세스 권한이 컴퓨터의 443 포트에 있는지 확인합니다.

로그는 각 Hybrid Worker의 로컬에 저장되며 위치는 C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes입니다.  Azure Automation에 역할을 온보딩하는 데 영향을 미치는 연결 또는 기타 문제가 있거나 정상 작업을 수행하는 동안 문제가 발생했음을 나타내는 경고 또는 오류 이벤트가 **Application and Services Logs\Microsoft SMA\Operations** 및 **Application and Services Logs\Operations Manager** 이벤트 로그에 기록되었는지 확인할 수 있습니다.  

## <a name="next-steps"></a>다음 단계

* [Hybrid Runbook Worker에서 Runbook 실행](automation-hrw-run-runbooks.md)을 검토하여 온-프레미스 데이터 센터 또는 다른 클라우드 환경의 프로세스를 자동화하도록 Runbook을 구성하는 방법을 알아봅니다.
* Hybrid Runbook Worker를 제거하는 방법의 지침은 [Azure Automation Hybrid Runbook Worker 제거](automation-remove-hrw.md)를 참조하세요.