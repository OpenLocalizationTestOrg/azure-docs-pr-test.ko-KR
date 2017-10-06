---
title: "Azure 자동화에서 aaaCertificate 자산 | Microsoft Docs"
description: "인증서는 runbook 또는 Azure 및 타사 리소스에 대해 DSC 구성 tooauthenticate 액세스할 수 있도록 Azure 자동화에 안전 하 게 저장할 수 있습니다.  이 문서에서는 인증서의 hello 세부 정보를 설명 방법과 텍스트와 그래픽 제작에 이러한 toowork 합니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: ac9c22ae-501f-42b9-9543-ac841cf2cc36
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/19/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 2c25bee937890438ea9022669be2c24c77a110b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="certificate-assets-in-azure-automation"></a>Azure 자동화의 인증서 자산

인증서에에서 저장할 수 안전 하 게 Azure 자동화 runbook 또는 hello를 사용 하 여 DSC 구성을 액세스할 수 있도록 **Get AzureRmAutomationRmCertificate** Azure 리소스 관리자 리소스에 대 한 작업입니다. 이 toocreate runbook 및 인증에 인증서를 사용 하는 DSC 구성을 사용 하면 또는 tooAzure 또는 타사 리소스를 추가 합니다.

> [!NOTE] 
> Azure 자동화의 안전한 자산에는 자격 증명, 인증서, 연결, 암호화된 변수 등이 있습니다. 이러한 자산 암호화 및 hello 각 자동화 계정에 대해 생성 되는 고유 키를 사용 하 여 Azure 자동화에에서 저장 됩니다. 이 키는 마스터 인증서로 암호화되어 Azure 자동화에 저장됩니다. 보안 자산을 저장 하기 전에 hello 자동화 계정에 대 한 hello 키 hello 마스터 인증서를 사용 하 여 암호가 해독 됩니다와 tooencrypt hello 자산을 사용 합니다.
> 

## <a name="windows-powershell-cmdlets"></a>Windows PowerShell cmdlet

다음 표에 hello의 hello cmdlet 사용 되는 toocreate 됩니다 하 고 Windows PowerShell을 사용 하 여 자동화 인증서 자산을 관리 합니다. Hello의 일부분으로 제공 [Azure PowerShell 모듈](../powershell-install-configure.md) 자동화 runbook 및 DSC 구성에 사용 하기 위해 사용할 수 있습니다.

|Cmdlet|설명|
|:---|:---|
|[Get AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx)|Runbook 또는 DSC 구성에서 인증서 toouse에 대 한 정보를 검색합니다. Get-automationcertificate 작업에서 hello 인증서 자체 에서만 검색할 수 있습니다.|
|[New-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603604.aspx)|Azure Automation으로 새 인증서를 만듭니다.|
[Remove-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603529.aspx)|Azure 자동화에서 인증서를 제거합니다.|Azure Automation으로 새 인증서를 만듭니다.
|[Set-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603760.aspx)|업로드 hello 인증서 파일 및.pfx에 대 한 hello 암호 설정 포함 하 여 기존 인증서에 대 한 hello 속성을 설정 합니다.|
|[Add-AzureCertificate](https://msdn.microsoft.com/library/azure/dn495214.aspx)|Hello에 대 한 서비스 인증서 업로드 클라우드 서비스를 지정 합니다.|


## <a name="creating-a-new-certificate"></a>새 인증서 만들기

새 인증서를 만들 때 자동화를.cer 또는.pfx 파일 tooAzure 업로드 합니다. Hello 인증서를 내보낼 수 있도록 표시 하는 경우 다음를 전송할 수 있습니다 hello Azure 자동화 인증서 저장소입니다. 내보낼 수 없는 경우 다음만 사용할 수 있습니다 hello runbook 또는 DSC 구성 내에서 서명에 합니다.


### <a name="toocreate-a-new-certificate-with-hello-azure-portal"></a>Azure 포털 hello로 새 인증서를 toocreate

1. 자동화 계정에서 클릭 hello **자산** 타일 tooopen hello **자산** 블레이드입니다.
1. Hello 클릭 **인증서** 타일 tooopen hello **인증서** 블레이드입니다.
1. 클릭 **인증서 추가** hello hello 블레이드 위쪽에 있습니다.
2. Hello에 hello 인증서에 대 한 이름을 입력 **이름** 상자입니다.
2. 클릭 **파일 선택** 아래 **인증서 파일 업로드** toobrowse.cer 또는.pfx 파일에 대 한 합니다.  .Pfx 파일을 선택 하는 경우 암호 및 여부 허용 하도록 내보낸 toobe를 지정 합니다.
1. 클릭 **만들기** toosave hello 새 인증서 자산입니다.


### <a name="toocreate-a-new-certificate-with-windows-powershell"></a>Windows PowerShell과 함께 새 인증서를 toocreate

hello 다음 예제에서는 어떻게 toocreate 새 자동화 인증서 하 고 내보낼 수 있도록 표시 합니다. 이 예제에서는 기존 .pfx 파일을 가져옵니다.

    $certName = 'MyCertificate'
    $certPath = '.\MyCert.pfx'
    $certPwd = ConvertTo-SecureString -String 'P@$$w0rd' -AsPlainText -Force
    $ResourceGroup = "ResourceGroup01"
    
    New-AzureRmAutomationCertificate -AutomationAccountName "MyAutomationAccount" -Name $certName -Path $certPath –Password $certPwd -Exportable -ResourceGroupName $ResourceGroup

## <a name="using-a-certificate"></a>인증서 사용

Hello를 사용 해야 **Get-automationcertificate** 활동 toouse 인증서입니다. Hello를 사용할 수 없습니다 [Get AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) cmdlet hello 인증서 자산 있지만 hello 인증서가 아닌 자체에 대 한 정보를 반환 하기 때문입니다.

### <a name="textual-runbook-sample"></a>텍스트 Runbook 샘플

다음 샘플 코드는 hello 인증서 tooa tooadd 클라우드 runbook에서 서비스 하는 방법을 보여 줍니다. 이 샘플에서는 hello 암호는 암호화 된 자동화 변수에서 검색 됩니다.

    $serviceName = 'MyCloudService'
    $cert = Get-AutomationCertificate -Name 'MyCertificate'
    $certPwd = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyCertPassword'
    Add-AzureCertificate -ServiceName $serviceName -CertToDeploy $cert

### <a name="graphical-runbook-sample"></a>그래픽 Runbook 샘플

추가한는 **Get-automationcertificate** hello 인증서 hello 그래픽 편집기 및 선택의 hello 라이브러리 창에서 마우스 오른쪽 단추로 클릭 하 여 그래픽 runbook tooa **toocanvas 추가**합니다.

![인증서 toohello 캔버스 추가](media/automation-certificates/automation-certificate-add-to-canvas.png)

hello 다음 이미지의 예가 나와 그래픽 runbook에서 인증서를 사용 합니다.  이 hello 텍스트 runbook에서 인증서 tooa 클라우드 서비스를 추가 하는 데 위에 표시 된 동일한 예입니다.

![그래픽 작성 예제 ](media/automation-certificates/graphical-runbook-add-certificate.png)


## <a name="next-steps"></a>다음 단계

- 활동의 링크 toocontrol hello 논리적 흐름 runbook 작업에 대 한 자세한 toolearn 설계 tooperform를 참조 [그래픽 제작에 대 한 링크](automation-graphical-authoring-intro.md#links-and-workflow)합니다. 
