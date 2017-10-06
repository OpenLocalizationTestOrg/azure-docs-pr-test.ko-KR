---
title: "자동화 Hybrid Runbook Worker aaaAzure | Microsoft Docs"
description: "이 문서에서는 설치 하 고 기능인 있습니다 toorun runbook 컴퓨터에서 로컬 데이터 센터 또는 클라우드 공급자에 있는 Azure 자동화 Hybrid Runbook Worker를 사용 하 여 설명 합니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 06227cda-f3d1-47fe-b3f8-436d2b9d81ee
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: magoedte;bwren
ms.openlocfilehash: ccee35e8324149a79ff692a867e5ce7801299bcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-resources-in-your-data-center-or-cloud-with-hybrid-runbook-worker"></a>Hybrid Runbook Worker를 사용하여 데이터 센터 또는 클라우드의 리소스 자동화
Azure 자동화의 Runbook hello Azure 클라우드에에서 실행 리소스의 다른 클라우드의 또는 온-프레미스 환경에 액세스할 수 없습니다.  hello 하이브리드 Runbook 작업자 Azure 자동화의 기능은 toorun runbook hello 역할을 호스팅하는 hello 컴퓨터에서 직접 및 hello 환경 toomanage의 리소스에 대 한 로컬 리소스입니다. Runbook 저장 하 고 Azure 자동화에서 관리 되는 고 그런 다음 tooone 또는 지정 된 컴퓨터에 더가 배달 됩니다.  

이 기능은 hello 다음 이미지에에서 표시 되어 있습니다.<br>  

![Hybrid Runbook Worker 개요](media/automation-offering-get-started/automation-infradiagram-networkcomms.png)

Hello 하이브리드 Runbook 작업자 역할 및 배포 고려 사항, 기술 개요를 참조 하십시오. [자동화 아키텍처 개요](automation-offering-get-started.md#automation-architecture-overview)합니다.    

## <a name="hybrid-runbook-worker-groups"></a>Hybrid Runbook Worker 그룹
각 Hybrid Runbook Worker hello 에이전트를 설치할 때 지정 된 Hybrid Runbook Worker 그룹의 구성원임을 확인 합니다.  그룹은 단일 에이전트를 포함할 수 있지만 고가용성을 위해 그룹에 여러 에이전트를 설치할 수 있습니다.

Hybrid Runbook Worker에서 runbook을 시작 하면 실행 되는 hello 그룹을 지정 합니다.  hello 그룹의 hello 멤버는 작업자 hello 요청 처리를 결정 합니다.  특정 작업자를 지정할 수 없습니다.

## <a name="relationship-tooservice-management-automation"></a>관계 tooService 관리 자동화
[서비스 관리 자동화 (SMA)](https://technet.microsoft.com/library/dn469260.aspx) 있습니다 toorun hello 로컬 데이터 센터에서 Azure 자동화에서 지원 되는 동일한 runbook입니다. SMA는 Windows Azure 팩이 SMA 관리를 위한 그래픽 인터페이스를 포함하므로 일반적으로 Windows Azure 팩과 함께 배포됩니다. Azure 자동화와는 달리 SMA 웹 서버 toohost hello API, 데이터베이스 toocontain runbook 및 SMA 구성 및 Runbook Worker tooexecute runbook 작업을 포함 하는 로컬 설치가 필요 합니다. Azure 자동화 hello 클라우드에서 이러한 서비스를 제공 하 고 하기만 하면 로컬 환경에서 Hybrid Runbook Worker toomaintain hello 합니다.

기존 SMA 사용자 인 경우 이동할 수 있습니다 변경 하지 않고 Hybrid Runbook Worker를 함께 사용 하 여 runbook tooAzure 자동화 toobe에 설명 된 대로 자체 인증 tooresources 작동 하는지 가정 [하이브리드 Runbook에서 runbook을 실행 합니다. 작업자](automation-hrw-run-runbooks.md)합니다.  SMA의 Runbook hello runbook에 대 한 인증을 제공할 수 있는 hello 작업자 서버에 대 한 hello 서비스 계정의 hello 컨텍스트에서 실행 됩니다.

Azure 자동화 Hybrid Runbook Worker 또는 서비스 관리 자동화와 요구 사항에 더 적절 한지 조건 toodetermine 다음 hello를 사용할 수 있습니다.

* SMA는 그래픽 관리 인터페이스를 필요한 경우 연결 된 Azure Pack tooWindows 있는 기본 구성 요소는 로컬 설치 되어 있어야 합니다. 많은 로컬 리소스는 로컬 Runbook Worker에 에이전트를 설치하기만 하면 되는 Azure Automation보다 높은 유지 관리 비용이 필요합니다. hello 에이전트 유지 관리 비용을 감소 하는 추가 Operations Management Suite에 의해 관리 됩니다.
* Azure 자동화 hello 클라우드에서 해당 runbook을 저장 하 고 tooon 온-프레미스 하이브리드 Runbook 작업자에 업데이트를 전달 합니다. 보안 정책에서 이 동작을 허용하지 않는 경우에는 SMA를 사용해야 합니다.
* SMA는 System Center에 포함되므로 System Center 2012 R2 라이선스가 필요합니다. Azure Automation은 계층화된 구독 모델을 기반으로 합니다.
* Azure Automation에는 SMA에서 사용할 수 없는 그래픽 Runbook 등의 고급 기능이 있습니다.

## <a name="installing-hello-windows-hybrid-runbook-worker"></a>Hello Windows Hybrid Runbook Worker를 설치합니다. 

tooinstall Windows 하이브리드 Runbook 작업자를 구성 하 고, 두 가지 방법이 있습니다 사용할 수 있습니다.  hello 메서드 runbook toocompletely 필요한 hello 프로세스를 자동화 하는 자동화를 사용 하는 것이 좋습니다 tooconfigure Windows 컴퓨터.  두 번째 방법은 hello 단계별 절차 toomanually 설치를 수행 하 고 hello 역할을 구성 합니다.  

> [!NOTE]
> tooadd 해야 toomanage hello 하이브리드 Runbook 작업자 역할이 있는 구성을 DSC (필요한 상태)를 지 원하는 서버 hello 구성, DSC 노드 것입니다.  DSC를 통한 관리를 위한 온보드에 대한 정보는 [Azure Automation DSC를 통한 관리를 위한 컴퓨터 온보드](automation-dsc-onboarding.md)를 참조하세요.           
><br>
>Hello를 사용 하도록 설정 하면 [업데이트 관리 솔루션](../operations-management-suite/oms-solution-update-management.md), 모든 Windows 컴퓨터 연결 tooyour OMS 작업 영역이이 솔루션에 포함 된 Hybrid Runbook Worker toosupport runbook으로 자동으로 구성 됩니다.  그러나 Automation 계정에서 이미 정의한 모든 Hybrid Worker 그룹에 등록되지 않았습니다.  hello 컴퓨터 추가할 수 있습니다 tooa Hybrid Runbook Worker 그룹 자동화 계정 toosupport 자동화 runbook의에서 hello 솔루션과 하이브리드 Runbook 작업자 그룹 멤버 자격 둘 다에 동일한 계정 hello를 사용 하는 상태로 합니다.  이 기능은 tooversion 7.2.12024.0 hello Hybrid Runbook Worker의 추가 되었습니다.  

Hello에 대 한 정보를 따라 검토 hello [하드웨어 및 소프트웨어 요구 사항](automation-offering-get-started.md#hybrid-runbook-worker) 및 [네트워크 준비에 대 한 정보](automation-offering-get-started.md#network-planning) Hybrid Runbook Worker 배포를 시작 하기 전에.  Runbook worker를 성공적으로 배포한 후 검토 [하이브리드 Runbook 작업자에서 실행할 runbook](automation-hrw-run-runbooks.md) toolearn tooconfigure runbook tooautomate 처리 하는 방법을 온-프레미스 데이터 센터 또는 다른 클라우드 환경에서 합니다.  
 
### <a name="automated-deployment"></a>자동화된 배포

Hello 다음이 수행 hello Windows 하이브리드 작업자 역할의 tooautomate hello 설치 및 구성 단계입니다.  

1. Hello 다운로드 *새로 OnPremiseHybridWorker.ps1* hello에서 스크립트 [PowerShell 갤러리](https://www.powershellgallery.com/packages/New-OnPremiseHybridWorker/1.0/DisplayScript) hello 하이브리드 Runbook 작업자 역할을 실행 하는 hello 컴퓨터에서 직접 또는 다른 컴퓨터에서 프로그램 환경 toohello 작업자를 복사 합니다.  

    hello *새로 OnPremiseHybridWorker.ps1* 스크립트 hello를 실행 하는 동안 매개 변수 뒤에 필요 합니다.

  * *AutomationAccountName* (필수)-hello 사용자의 자동화 계정 이름입니다.  
  * *ResourceGroupName* (필수)-자동화 계정에 연결 된 hello 리소스 그룹의 hello 이름입니다.  
  * *HybridGroupName* (필수)-이 시나리오를 지 원하는 hello runbook에 대 한 대상으로 지정 하는 하이브리드 Runbook 작업자 그룹의 hello 이름입니다. 
  *  *SubscriptionID* (필수)-hello 자동화 계정에 있는 Azure 구독 Id입니다.
  *  *WorkspaceName* (선택 사항)-hello OMS 작업 영역 이름입니다.  OMS 작업 영역이 hello 스크립트 만들고 하나를 구성 합니다.  

     > [!NOTE]
     > 현재 hello OMS와의 통합에 대 한 지원 되는 유일한 자동화 영역은- **오스트레일리아 남동부**, **미국 동부 2**, **동남 아시아**, 및 **서 부 유럽**합니다.  자동화 계정을 해당 영역 중 하나에 없는 경우 hello 스크립트 OMS 작업 영역 만들지만 메시지를 표시 하 고 없습니다 함께 연결 합니다.
     > 
2. 사용자 컴퓨터에서 시작 **Windows PowerShell** hello에서 **시작** 관리자 모드에서 화면입니다.  
3. PowerShell 명령줄 셸 hello에서 다운로드 하 고 매개 변수에 대 한 hello 값을 변경 하 고 실행 하는 hello 스크립트가 들어 있는 toohello 폴더 이동 *-AutomationAccountName*, *-ResourceGroupName* , *-HybridGroupName*, *-SubscriptionId*, 및 *-WorkspaceName*합니다.

     > [!NOTE] 
     > Hello 스크립트를 실행 한 후 Azure 사용한 메시지 표시 tooauthenticate 됩니다.  하면 **해야** hello 구독 관리자 역할의 멤버 및 hello 구독의 공동 관리자 인 계정으로 로그인 합니다.  
     >  
    
        .\New-OnPremiseHybridWorker.ps1 -AutomationAccountName <NameofAutomationAccount> `
        -ResourceGroupName <NameofOResourceGroup> -HybridGroupName <NameofHRWGroup> `
        -SubscriptionId <AzureSubscriptionId> -WorkspaceName <NameOfOMSWorkspace>

4. 입력 정보 요청된 tooagree tooinstall는 **NuGet** 되며 사용자 입력 정보 요청된 tooauthenticate Azure 자격 증명을 사용 합니다.<br><br> ![New-OnPremiseHybridWorker 스크립트 실행](media/automation-hybrid-runbook-worker/new-onpremisehybridworker-scriptoutput.png)

5. Hello 스크립트가 완료 되 면 hello 새 그룹을 만들고 구성원 수가 hello Hybrid Worker 그룹 블레이드가 표시 됩니다 또는 hello 멤버 수가 증가 하는 경우 기존 그룹입니다.  Hello 그룹 hello hello 목록에서 선택할 수 있습니다 **Hybrid Worker 그룹** 블레이드에 대 한 선택 hello **Hybrid Worker** 바둑판식으로 배열입니다.  Hello에 **Hybrid Worker** 블레이드에 나열 된 hello 그룹의 각 구성원 표시 합니다.  

### <a name="manual-deployment"></a>수동 배포 
자동화 환경에 한 번씩 hello 처음 두 단계를 수행 하 고 hello 남아 있는 각 작업자 컴퓨터에 대 한 단계를 반복 합니다.

#### <a name="1-create-operations-management-suite-workspace"></a>1. Operations Management Suite 작업 영역 만들기
Operations Management Suite 작업 영역이 아직 없는 경우 [작업 영역 관리](../log-analytics/log-analytics-manage-access.md)의 지침에 따라 작업 영역을 만듭니다. 이미 있는 경우에는 기존 작업 영역을 사용할 수 있습니다.

#### <a name="2-add-automation-solution-toooperations-management-suite-workspace"></a>2. 자동화 솔루션 tooOperations Management Suite 작업 영역 추가
솔루션 추가 기능 tooOperations 관리 제품군을 사용 합니다.  자동화 솔루션 hello Azure 자동화 Hybrid Runbook Worker에 대 한 지원을 비롯 하 여에 대 한 기능을 추가 합니다.  Hello 솔루션 tooyour 작업 영역에 추가 하면 자동으로 hello 다음 단계에서 설치 하는 작업자 구성 요소 toohello 에이전트 컴퓨터 아래로 밀어냅니다.

Hello 지침에 따라 [tooadd hello 솔루션 갤러리를 사용 하는 솔루션](../log-analytics/log-analytics-add-solutions.md) tooadd hello **자동화** 솔루션 tooyour Operations Management Suite 작업 영역입니다.

#### <a name="3-install-hello-microsoft-monitoring-agent"></a>3. Hello Microsoft Monitoring Agent 설치
Microsoft Monitoring Agent hello 컴퓨터 tooOperations Management Suite에 연결합니다.  온-프레미스 컴퓨터에 hello 에이전트를 설치 하 고 tooyour 작업 영역 연결 될 때 자동으로 다운로드 Hybrid Runbook Worker에 필요한 hello 구성 요소입니다.

Hello 지침에 따라 [연결 Windows 컴퓨터 tooLog 분석](../log-analytics/log-analytics-windows-agents.md) hello 온-프레미스 컴퓨터에서 tooinstall hello 에이전트입니다.  다중 작업자 tooyour 환경의 여러 컴퓨터 tooadd에 대 한이 과정을 반복할 수 있습니다.

Hello에 나타날 것 hello 에이전트에 tooOperations Management Suite에 연결 하는 경우 **연결 된 원본** hello Operations Management Suite 탭 **설정을** 창.  이라는 폴더에 있을 때 해당 hello 에이전트에서 hello 자동화 솔루션을 다운로드 올바르게 확인할 수 있습니다 **AzureAutomationFiles** C:\Program Files\Microsoft Monitoring Agent\Agent에 있습니다.  Hybrid Runbook Worker hello tooconfirm hello 버전에서는 tooC:\Program Files\Microsoft Agent\Agent\AzureAutomation\ 모니터링 및 참고 hello 탐색할 수 있습니다 \\ *버전* 하위 폴더입니다.   

#### <a name="4-install-hello-runbook-environment-and-connect-tooazure-automation"></a>4. Hello runbook 환경을 설치 하 고 tooAzure 자동화 연결
자동화 솔루션 hello hello 아래로 밀어냅니다 에이전트 tooOperations 관리 제품군을 추가 하면 **HybridRegistration** hello를 포함 하는 PowerShell 모듈 **Add-hybridrunbookworker** cmdlet.  이 cmdlet tooinstall hello runbook 환경 hello 컴퓨터에서 사용 하 여 Azure 자동화에 등록 하십시오.

관리자 모드에서 PowerShell 세션을 열고 다음 명령을 tooimport hello 모듈 hello를 실행 합니다.

    cd "C:\Program Files\Microsoft Monitoring Agent\Agent\AzureAutomation\<version>\HybridRegistration"
    Import-Module HybridRegistration.psd1

그러고 나 서 hello **Add-hybridrunbookworker** 구문 다음 hello를 사용 하 여 cmdlet:

    Add-HybridRunbookWorker –GroupName <String> -EndPoint <Url> -Token <String>

Hello에서이 cmdlet에 필요한 hello 정보를 읽을 수 **키 관리** 블레이드 hello Azure 포털의에서.  Hello를 선택 하 여이 블레이드를 엽니다 **키** hello에서 옵션 **설정을** 블레이드 자동화 계정에서 합니다.

![Hybrid Runbook Worker 개요](media/automation-hybrid-runbook-worker/elements-panel-keys.png)

* **GroupName** hello hello Hybrid Runbook Worker 그룹 이름입니다. 이 그룹에 이미 있으면 hello 자동화 계정에서 tooit hello 현재 컴퓨터에 추가 됩니다.  그렇지 않으면 이 그룹이 추가됩니다.
* **끝점** 는 hello **URL** 필드 hello에 **키 관리** 블레이드입니다.
* **토큰** 는 hello **기본 액세스 키** hello에 **키 관리** 블레이드입니다.  

사용 하 여 hello **-Verbose** 바꾸십시오 **Add-hybridrunbookworker** tooreceive 자세한 hello 설치에 대 한 정보입니다.

#### <a name="5-install-powershell-modules"></a>5. PowerShell 모듈 설치
Runbook은 hello 활동 및 Azure 자동화 환경에 설치 된 hello 모듈에 정의 된 cmdlet을 사용할 수 있습니다.  이러한 모듈 되지 않으므로 배포가 자동으로 tooon 온-프레미스 컴퓨터 그러나 수동으로 설치 해야 합니다.  hello 예외는 hello Azure 자동화에 대 한 모든 Azure 서비스와 작업에 대 한 액세스 toocmdlets를 제공 하는 기본적으로 설치 되는 Azure 모듈입니다.

Hello Hybrid Runbook Worker 기능의 주요 목적은 hello toomanage 로컬 리소스 이므로, 가장 가능성이 높은 해야 이러한 리소스를 지 원하는 tooinstall hello 모듈.  너무 참조할 수[모듈 설치](http://msdn.microsoft.com/library/dd878350.aspx) Windows PowerShell 모듈을 설치에 대 한 내용은 합니다.  설치 된 모듈을 hello Hybrid worker에서 자동으로 가져올 수 있도록 PSModulePath 환경 변수에서 참조 하는 위치에 있어야 합니다.  자세한 내용은 참조 하십시오. [수정 hello PSModulePath 설치 경로](https://msdn.microsoft.com/library/dd878326%28v=vs.85%29.aspx)합니다. 

## <a name="removing-hybrid-runbook-worker"></a>Hybrid Runbook Worker 제거 
그룹에서 하나 이상의 Hybrid Runbook Worker를 제거할 수 있습니다 또는 요구 사항에 따라 hello 그룹을 제거할 수 있습니다.  온-프레미스 컴퓨터에서 Hybrid Runbook Worker tooremove hello 다음 단계를 수행 합니다.

1. Hello Azure 포털에서에서 tooyour 자동화 계정을 이동 합니다.  
2. Hello에서 **설정** 블레이드를 **키** 필드에 대 한 hello 값을 기록 하 고 **URL** 및 **기본 액세스 키**합니다.  이 정보는 hello 다음 단계에 필요 합니다.
3. 관리자 모드에서 PowerShell 세션을 열고 hello 다음 실행 명령- `Remove-HybridRunbookWorker -url <URL> -key <PrimaryAccessKey>`합니다.  사용 하 여 hello **-Verbose** hello 제거 프로세스의 자세한 로그에 대 한 전환 합니다.

> [!NOTE]
> Hello 컴퓨터 hello 기능과 hello 하이브리드 Runbook 작업자 역할의 구성에서에서 Microsoft Monitoring Agent hello를 제거 되지 않습니다.  

## <a name="remove-hybrid-worker-groups"></a>Hybrid Worker 그룹 제거
그룹 tooremove 먼저 이전에 표시 된 hello 프로시저를 사용 하 여 hello 그룹의 멤버인 모든 컴퓨터에서 Hybrid Runbook Worker tooremove hello을 후 hello 단계 tooremove hello 그룹 다음을 수행 합니다.  

1. Hello Azure 포털에서에서 자동화 계정을 hello를 엽니다.
2. 선택 hello **Hybrid Worker 그룹** 타일 및 hello **Hybrid Worker 그룹** 블레이드, toodelete 선택 hello 그룹입니다.  Hello 특정 그룹을 선택한 후 hello **Hybrid worker 그룹** 속성 블레이드 표시 됩니다.<br> ![Hybrid Runbook Worker 그룹 블레이드](media/automation-hybrid-runbook-worker/automation-hybrid-runbook-worker-group-properties.png)   
3. Hello 선택한 그룹에 대 한 hello 속성 블레이드에서 클릭 **삭제**합니다.  ֲ ¸  묻는 있습니다 tooconfirm이이 작업을 선택 **예** ख ा त tooproceed 하려는 경우.<br> ![그룹 삭제 확인 대화 상자](media/automation-hybrid-runbook-worker/automation-hybrid-runbook-worker-confirm-delete.png)<br> 이 프로세스는 몇 가지 걸릴 수 초 toocomplete 하 고 아래에서 해당 진행률을 추적할 수 **알림** hello 메뉴에서 합니다.  

## <a name="troubleshooting"></a>문제 해결 
Hybrid Runbook Worker hello에 따라 달라 집니다 hello 프로그램 자동화 계정 tooregister hello 작업자와 Microsoft Monitoring Agent toocommunicate, 수신 runbook 작업 및 상태를 보고 합니다. Hello 작업자의 등록에 실패 하면 hello 오류에 대 한 몇 가지 원인은 다음과 같습니다.  

1. 프록시 또는 방화벽 뒤에 있는 hello 하이브리드 작업자가입니다.  
    Hello 컴퓨터는 포트 443에서 아웃 바운드 액세스 too*.azure automation.net 확인 합니다.  

2. hello 컴퓨터 hello 하이브리드 작업자에서 실행 되 고 적습니다 hello 최소 하드웨어 보다 [요구 사항](automation-offering-get-started.md#hybrid-runbook-worker)합니다.  
    Hybrid Runbook Worker 충족 해야 하는 hello를 실행 하는 컴퓨터는 최소 하드웨어 요구 사항을 toohost 지정 하기 전에 hello이 기능입니다. 그렇지 않은 경우 다른 백그라운드 프로세스 및 실행 하는 동안 runbook에서 발생 한 경합 hello 리소스 사용률을 따라 hello 컴퓨터 됩니다 될 과도 하 게 및 runbook 작업 지연 또는 시간 초과 발생 합니다.
   Hello 컴퓨터 toorun hello Hybrid Runbook Worker 기능 지정 hello 최소 하드웨어 요구 사항을 충족 하는지 확인 합니다.  그렇지 않으면 CPU 및 메모리 사용률 toodetermine 하이브리드 Runbook 작업자 프로세스의 성능을 hello와 Windows 간에 상관 관계를 모니터링 합니다.  메모리 또는 CPU 부담이 있는 경우이 hello 필요 tooupgrade을 나타내거나 추가 프로세서를 추가할 수 있습니다 또는 증가 메모리 tooaddress hello 리소스 병목 상태가 발생 하 고 hello 오류를 해결 합니다. 또는 작업 부하 요구 증가 되기 나타낼 때의 크기를 조정 하 고 hello 최소 요구 사항을 지원할 수 있는 다른 컴퓨터 리소스를 선택 합니다.
    
3. hello Microsoft Monitoring Agent 서비스가 실행 되지 않습니다.  
    Hello Microsoft 모니터링 에이전트 Windows 서비스가 실행 되지 않는 경우이 Hybrid Runbook Worker hello Azure 자동화와의 통신을 방지 합니다.  Hello 다음 powershell에서 명령을 입력 하 여 hello 에이전트가 실행 중인지 확인: `get-service healthservice`합니다.  Hello 서비스가 중지 되 면 hello 다음 PowerShell toostart hello 서비스에 명령을 입력: `start-service healthservice`합니다.  

4. Hello에 **응용 프로그램 및 서비스 Logs\Operations 관리자** 이벤트 로그 이벤트 4502 EventMessage 포함 하 고 참조 **Microsoft.EnterpriseManagement.HealthService.AzureAutomation.HybridAgent**설명 뒤 hello로: *hello 서비스에서 제공 하는 hello 인증서 <wsid>. oms.opinsights.azure.com Microsoft 서비스에 사용 되는 인증 기관에서 발급 되지 않았습니다. TLS/SSL 통신을 차단 하는 프록시를 실행 하는 경우 네트워크 관리자 toosee에 게 문의 하십시오. hello 문서 k b 3126513에 연결 문제에 대 한 추가 문제 해결 정보가 있습니다.*
    이 프로그램 프록시 또는 네트워크 방화벽 blockking 통신 tooMicrosoft Azure에서 발생할 수 있습니다.  Hello 컴퓨터 포트 443에서 아웃 바운드 액세스 too*.azure automation.net에 확인 합니다.

로그는 각 Hybrid Worker의 로컬에 저장되며 위치는 C:\ProgramData\Microsoft\System Center\Orchestrator\7.2\SMA\Sandboxes입니다.  모든 경고 또는 오류 이벤트 toohello 작성 되는지 확인할 수 있습니다 **응용 프로그램 및 서비스 Logs\Microsoft SMA\Operations** 및 **응용 프로그램 및 서비스 Logs\Operations 관리자** 이벤트 로그에 필요한 연결이 나 정상 작업을 수행 하는 동안 온 보 딩 hello 역할 tooAzure 자동화 또는 문제의 영향을 주는 기타 문제를 나타냅니다.  

## <a name="next-steps"></a>다음 단계
검토 [하이브리드 Runbook 작업자에서 실행할 runbook](automation-hrw-run-runbooks.md) toolearn 어떻게 tooconfigure runbook tooautomate는 온-프레미스 데이터 센터 또는 다른 클라우드 환경에서을 처리 합니다.
