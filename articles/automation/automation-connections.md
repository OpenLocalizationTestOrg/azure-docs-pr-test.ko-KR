---
title: "Azure 자동화에서 aaaConnection 자산 | Microsoft Docs"
description: "Azure 자동화에서 연결 자산 runbook 또는 DSC 구성에서 응용 프로그램 또는 hello 필요한 정보 tooconnect tooan 외부 서비스를 포함합니다. 이 문서에서는 연결의 hello 세부 정보를 설명 방법과 텍스트와 그래픽 제작에 이러한 toowork 합니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: f0239017-5c66-4165-8cca-5dcb249b8091
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/13/2017
ms.author: magoedte; bwren
ms.openlocfilehash: f0f6b9fb960789b34af7b60eb1069313fdcf071c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connection-assets-in-azure-automation"></a>Azure 자동화의 연결 자산

자동화 연결 자산 runbook 또는 DSC 구성에서 응용 프로그램 또는 hello 필요한 정보 tooconnect tooan 외부 서비스를 포함합니다. 이 사용자 이름 및 URL 또는 포트와 같은 추가 tooconnection 정보에는 암호 등 인증에 필요한 정보를 포함할 수 있습니다. 연결의 hello 값은 tooa 특정 응용 프로그램 단일 자산에서 것과 반대로 toocreating으로 연결 하기 위한 hello 속성의 모든 변수를 여러 개 유지 합니다. hello 사용자를 한 곳에서 연결에 대 한 hello 값 편집 하 고 단일 매개 변수 연결 tooa runbook 또는 DSC 구성의 hello 이름을 전달할 수 있습니다. hello runbook 또는 hello로 DSC 구성에는 연결에 액세스할 수에 대 한 속성을 hello **Get-automationconnection** 활동입니다.

연결을 만들 때 *연결 형식*을 지정해야 합니다. hello 연결 유형은 속성 집합을 정의 하는 템플릿입니다. hello 연결은 해당 연결 유형에 정의 된 각 속성에 대 한 값을 정의 합니다. 연결 유형에 통합 모듈에서 추가한 tooAzure 자동화 또는 hello를 사용 하 여 만든 [Azure 자동화 API](http://msdn.microsoft.com/library/azure/mt163818.aspx) hello 통합 모듈에 연결 유형이 포함 되 고 자동화 계정으로 가져온 경우. 그렇지 않으면 메타 데이터 파일 toospecify 자동화 연결 형식 toocreate가 필요 합니다.  이와 관련된 자세한 내용은 [통합 모듈](automation-integration-modules.md)을 참조하세요.  

>[!NOTE] 
>Azure 자동화의 안전한 자산에는 자격 증명, 인증서, 연결, 암호화된 변수 등이 있습니다. 이러한 자산 암호화 및 hello 각 자동화 계정에 대해 생성 되는 고유 키를 사용 하 여 Azure 자동화에에서 저장 됩니다. 이 키는 마스터 인증서로 암호화되어 Azure 자동화에 저장됩니다. 보안 자산을 저장 하기 전에 hello 자동화 계정에 대 한 hello 키 hello 마스터 인증서를 사용 하 여 암호가 해독 됩니다와 tooencrypt hello 자산을 사용 합니다.

## <a name="windows-powershell-cmdlets"></a>Windows PowerShell cmdlet

다음 표에 hello의 hello cmdlet 사용 되는 toocreate 되며 자동화 연결 Windows PowerShell로 관리할 수 있습니다. Hello의 일부분으로 제공 [Azure PowerShell 모듈](/powershell/azure/overview) 자동화 runbook 및 DSC 구성에 사용 하기 위해 사용할 수 있습니다.

|Cmdlet|설명|
|:---|:---|
|[Get-AzureRmAutomationConnection](/powershell/module/azurerm.automation/get-azurermautomationconnection)|연결을 검색합니다. Hello 연결 필드의 hello 값으로 해시 테이블을 포함합니다.|
|[New-AzureRmAutomationConnection](/powershell/module/azurerm.automation/new-azurermautomationconnection)|새 연결을 만듭니다.|
|[Remove-AzureRmAutomationConnection](/powershell/module/azurerm.automation/remove-azurermautomationconnection)|기존 연결을 제거합니다.|
|[Set-AzureRmAutomationConnectionFieldValue](/powershell/module/azurerm.automation/set-azurermautomationconnectionfieldvalue)|기존 연결에 대 한 특정 필드의 hello 값을 설정합니다.|

## <a name="activities"></a>활동

다음 표에 hello의 hello 활동 runbook 또는 DSC 구성에서 사용 되는 tooaccess 연결이 있습니다.

|활동|설명|
|---|---|
|[Get-AutomationConnection](/powershell/module/azure/get-azureautomationconnection?view=azuresmps-3.7.0)|연결 toouse를 가져옵니다. Hello 연결의 hello 속성이 있는 해시 테이블을 반환합니다.|

>[!NOTE] 
>사용 하 여 변수를 사용 하면 안 hello – Name 매개 변수에 **Get-AutomationConnection** 디자인 타임에 runbook 또는 DSC 구성 및 연결 자산 간의 종속성을 검색 하기가 어려워질 수 있습니다.

## <a name="creating-a-new-connection"></a>새 연결 만들기

### <a name="toocreate-a-new-connection-with-hello-azure-portal"></a>새 연결 hello Azure 포털을 toocreate

1. 자동화 계정에서 클릭 hello **자산** 부분 tooopen hello **자산** 블레이드입니다.
2. Hello 클릭 **연결** 부분 tooopen hello **연결** 블레이드입니다.
3. 클릭 **연결 추가** hello hello 블레이드 위쪽에 있습니다.
4. Hello에 **형식** 선택 hello 형식 드롭다운에서 원하는 toocreate 연결의 합니다. hello 폼은 해당 특정 형식에 대 한 hello 속성을 제공 합니다.
5. Hello 양식을 작성 하 고 클릭 **만들기** toosave hello 새 연결 합니다.

### <a name="toocreate-a-new-connection-with-hello-azure-classic-portal"></a>새 연결 hello Azure 클래식 포털을 toocreate

1. 자동화 계정에서 클릭 **자산** hello 창의 위쪽에 hello 합니다.
2. Hello hello 창의 아래쪽에 있는 클릭 **설정 추가**합니다.
3. **연결 추가**를 클릭합니다.
4. Hello에 **연결 유형** 선택 hello 형식 드롭다운에서 원하는 toocreate 연결의 합니다.  hello 마법사는 해당 특정 형식에 대 한 hello 속성을 제공 합니다.
5. Hello 마법사를 완료 하 고 hello 확인란 toosave hello 새 연결을 클릭 합니다.

### <a name="toocreate-a-new-connection-with-windows-powershell"></a>Windows PowerShell과 함께 새 연결 toocreate

Hello를 사용 하 여 Windows PowerShell과 함께 새 연결을 만듭니다 [새로 AzureRmAutomationConnection](/powershell/module/azurerm.automation/new-azurermautomationconnection) cmdlet. 이 cmdlet의 매개 변수 이름 **ConnectionFieldValues** 예상 되는 [해시 테이블](http://technet.microsoft.com/library/hh847780.aspx) 각 hello 연결 형식이 정의 하는 hello 속성에 대 한 값을 정의 합니다.

자동화 hello로 잘 알고 있다면 [실행 계정을](automation-sec-configure-azure-runas-account.md) tooauthenticate runbook hello 서비스 사용자를 사용 하 여 hello 대체 toocreating hello hello hello 포털에서 다음 계정으로 실행 계정으로 제공 되는 PowerShell 스크립트 다음 명령 예제는 hello를 사용 하 여 새 연결 자산을 만듭니다.  

    $ConnectionAssetName = "AzureRunAsConnection"
    $ConnectionFieldValues = @{"ApplicationId" = $Application.ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Cert.Thumbprint; "SubscriptionId" = $SubscriptionId}
    New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $AutomationAccountName -Name $ConnectionAssetName -ConnectionTypeName AzureServicePrincipal -ConnectionFieldValues $ConnectionFieldValues 

Hello 연결 형식과 함께 기본적으로 몇 가지 전역 모듈 자동화 계정을 만들 때 자동으로 포함 수 toouse hello 스크립트 toocreate hello 연결 자산 되므로 **AzurServicePrincipal**toocreate hello **AzureRunAsConnection** 연결 자산입니다.  을 염두에 중요 한 tookeep 다른 인증 방법으로 toocreate 새 연결 자산 tooconnect tooa 서비스 또는 응용 프로그램을 시도 하면 실패 합니다 hello 연결 유형에 자동화 계정에서 이미 정의 되어 있지 않으므로 때문입니다.  Toocreate 자체 연결 입력 하는 방법을 사용자 지정 또는 hello에서 모듈에 대 한 자세한 내용은 [PowerShell 갤러리](https://www.powershellgallery.com), 참조 [통합 모듈](automation-integration-modules.md)
  
## <a name="using-a-connection-in-a-runbook-or-dsc-configuration"></a>runbook 또는 DSC 구성에서 연결 사용하기

Runbook 또는 hello로 DSC 구성에서 연결을 검색 **Get-automationconnection** cmdlet.  Hello를 사용할 수 없습니다 [Get AzureRmAutomationConnection](https://docs.microsoft.com/powershell/resourcemanager/azurerm.automation/v1.0.12/Get-AzureRmAutomationConnection?redirectedfrom=msdn) 활동입니다.  이 활동 hello hello 연결의 다른 필드의 hello 값을 검색 하 고로 반환 된 [해시 테이블](http://go.microsoft.com/fwlink/?LinkID=324844) hello hello runbook 또는 DSC 구성에 적절 한 명령을 사용 하 여 다음 사용할 수 있는 합니다.

### <a name="textual-runbook-sample"></a>텍스트 Runbook 샘플

hello 다음 샘플 명령은 표시 방법을 toouse hello 실행 계정을 앞에서 언급 한, runbook의 Azure 리소스 관리자 리소스와 tooauthenticate 합니다.  Hello 연결을 사용 하 여 hello 계정으로 실행 계정을 나타내는, hello 인증서 기반 서비스 사용자를 참조 하는 자산 하지 자격 증명입니다.  

    $Conn = Get-AutomationConnection -Name AzureRunAsConnection 
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint 

### <a name="graphical-runbook-samples"></a>그래픽 Runbook 샘플

추가한는 **Get-automationconnection** hello 그래픽 편집기 및 선택의 hello 라이브러리 창에서 hello 연결을 마우스 오른쪽 단추로 클릭 하 여 활동 tooa 그래픽 runbook **toocanvas 추가**합니다.

![](media/automation-connections/connection-add-canvas.png)

hello 다음 이미지의 예가 나와 그래픽 runbook에서 연결을 사용 합니다.  이 hello 텍스트 runbook hello 계정으로 실행 계정을 사용 하 여 인증을 위해 위에 표시 된 동일한 예입니다.  Hello를 사용 하는이 예제 **상수 값** hello에 대 한 데이터 집합 **RunAs 연결 가져오기** 인증에 대 한 연결 개체를 사용 하는 활동입니다.  A [파이프라인 링크가](automation-graphical-authoring-intro.md#links-and-workflow) hello ServicePrincipalCertificate 매개 변수 집합은 단일 개체를 예상 하는 이후 여기에 사용 됩니다.

![](media/automation-connections/automation-get-connection-object.png)

## <a name="next-steps"></a>다음 단계

- 검토 [그래픽 제작에 대 한 링크](automation-graphical-authoring-intro.md#links-and-workflow) toounderstand hello toodirect 및 제어에 runbook 논리의 흐름 방식입니다.  

- 통합 모듈 내의 Azure 자동화로 직접 PowerShell 모듈 toowork를 만들기 위한 PowerShell 모듈 및 모범 사례 Azure 자동화 사용에 대 한 더 toolearn 참조 [통합 모듈](automation-integration-modules.md)합니다.  
