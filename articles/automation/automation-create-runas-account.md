---
title: "Azure 자동화 계정으로 실행 계정 aaaCreate | Microsoft Docs"
description: "이 문서에서는 설명 방법을 tooupdate 자동화 계정 및 hello 포털 또는 powershell을 실행 계정을 만듭니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/27/2017
ms.author: magoedte
ms.openlocfilehash: 94eb54fa0b518056a726d17146c63411e248273b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-automation-account-authentication-with-run-as-accounts"></a>실행 계정으로 Automation 계정 인증 업데이트 
Hello 포털에서 기존 자동화 계정을 업데이트 하거나 경우 PowerShell을 사용 하 여 수 있습니다.

* 자동화 계정을 만들지만 toocreate hello 계정으로 실행을 거부 합니다.
* 자동화 계정 toomanage 리소스 관리자 리소스를 이미 사용 중이 고 tooupdate hello 계정 tooinclude hello 실행 계정을 runbook 인증에 대 한 합니다.
* 자동화 계정 toomanage 클래식 리소스를 이미 사용 중이 고 tooupdate 것 toouse hello 클래식 실행 계정 대신 새 계정을 만들고 runbook과 자산 tooit 마이그레이션.   
* Toocreate 실행 하 고 기본 실행 계정을 사용 하 여 원하는 엔터프라이즈 인증 기관 (CA)에서 발급 한 인증서입니다.

## <a name="prerequisites"></a>필수 조건

* Azure 리소스 관리자 모듈 3.0.0 때 Windows 10 및 Windows Server 2016에만 실행 이상을 hello 스크립트 될 수 있습니다. 이전 버전의 Windows에서는 지원되지 않습니다.
* Azure PowerShell 1.0 이상 PowerShell 1.0 hello 릴리스에 대 한 자세한 내용은 참조 하십시오. [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azureps-cmdlets-docs)합니다.
* Hello에 대 한 hello 값으로 참조 하는 자동화 계정을 *– AutomationAccountName* 및 *-ApplicationDisplayName* hello PowerShell 스크립트 뒤에 매개 변수입니다.

tooget hello에 대 한 값 *SubscriptionID*, *ResourceGroup*, 및 *AutomationAccountName*, hello 스크립트에 대 한 필수 매개 변수는, 다음 hello지 않습니다.

1. Hello Azure 포털에서 hello에서 자동화 계정을 선택 **자동화 계정** 블레이드에서 다음을 선택 하 고 **모든 설정을**합니다.  
2. Hello에 **모든 설정을** 블레이드 아래 **계정 설정**선택, **속성**합니다. 
3. Hello에 hello 값을 기록 **속성** 블레이드입니다.<br><br> ![hello 자동화 계정 "속성" 블레이드](media/automation-create-runas-account/automation-account-properties.png)  

### <a name="required-permissions-tooupdate-your-automation-account"></a>필요한 사용 권한을 tooupdate 자동화 계정
자동화 계정을 tooupdate 있어야 다음 특정 권한을 hello 및이 항목 toocomplete 필요한 사용 권한.   
 
* AD 사용자 계정의 Microsoft.Automation 리소스에 대 한 사용 권한 해당 toohello 참가자 역할을 가진 toobe 추가 tooa 역할 문서에 설명 된 대로 필요한 [Azure 자동화에서 역할 기반 액세스 제어](automation-role-based-access-control.md#contributor-role-permissions)합니다.  
* Azure AD 테 넌 트의 관리자가 아닌 사용자 수 [AD 응용 프로그램 등록](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions) hello 응용 프로그램 등록 설정 너무 설정 되어 있으면**예**합니다.  Hello 응용 프로그램 등록 설정 너무 설정 되어 있으면**아니요**,이 작업을 수행 하는 hello 사용자는 Azure ad에서 전역 관리자 여야 합니다. 

가 아닌 hello 구독 Active Directory 인스턴스에서 소속 toohello 전역 관리자/공동 관리자의 역할 hello 구독을 추가 하기 전에 사용자 tooActive 디렉터리에 게스트로 추가 됩니다. 이 경우에는 "없는 사용 권한을 toocreate..." 표시 hello에 경고 **자동화 계정 추가** 블레이드입니다. 먼저 hello 구독 Active Directory 인스턴스에서 제거할 수도 있고 toomake 다시 추가 toohello 전역 관리자/공동 관리자 역할에 추가 된 사용자를 해당 Active Directory에서 전체 사용자입니다. tooverify hello에서 이러한 경우 **Azure Active Directory** hello Azure 포털의에서 창 **사용자 및 그룹**선택, **모든 사용자에 게** 및 hello를 선택한 후 특정 사용자 **프로필**합니다. 값의 hello hello **사용자 유형** hello 사용자 프로필 아래에 특성 같지 해야 **게스트**합니다.

## <a name="create-run-as-account-from-hello-portal"></a>Hello 포털에서 다음 계정으로 실행 계정을 만들려면
이 섹션에서는 다음 단계 tooupdate hello를 hello Azure 포털에서에서 Azure 자동화 계정을 수행 합니다.  Hello 계정으로 실행 및 기존 실행 계정을 개별적으로 만들고 hello 클래식 Azure 포털에서 toomanage 리소스 필요가 없는 경우 hello Azure 실행 계정만 만들 수 있습니다.  

hello 프로세스 hello 다음 자동화 계정에서 항목을 만듭니다.

**실행 계정의 경우:**

* 자체 서명 된 인증서로 Azure AD 응용 프로그램을 만듭니다, 그리고 hello 응용 프로그램에 대 한 서비스 주체 계정을 Azure AD에서 만들어지고 hello 계정 현재 구독에 대 한 hello 참가자 역할 할당 됩니다. 이 설정은 tooOwner 또는 다른 역할을 변경할 수 있습니다. 자세한 내용은 [Azure Automation의 역할 기반 액세스 제어](automation-role-based-access-control.md)를 참조하세요.
* 명명 된 자동화 인증서 자산을 만듭니다 *AzureRunAsCertificate* hello 자동화 계정을 지정 합니다. hello 인증서 자산 hello Azure AD 응용 프로그램에서 사용 되는 hello 인증서 개인 키를 보유 합니다.
* 명명 된 자동화 연결 자산을 만듭니다 *AzureRunAsConnection* hello 자동화 계정을 지정 합니다. hello applicationId, tenantId, subscriptionId, 및 인증서 지문을 hello 연결 자산을 보유합니다.

**클래식 실행 계정의 경우:**

* 명명 된 자동화 인증서 자산을 만듭니다 *AzureClassicRunAsCertificate* hello 자동화 계정을 지정 합니다. hello 인증서 자산 hello 관리 인증서에 의해 사용 된 hello 인증서 개인 키를 보유 합니다.
* 명명 된 자동화 연결 자산을 만듭니다 *AzureClassicRunAsConnection* hello 자동화 계정을 지정 합니다. hello 연결 자산 hello 구독 이름, subscriptionId, 이름과 인증서 자산을 보유합니다.

1. Hello 구독 관리자 역할의 멤버 및 hello 구독의 공동 관리자 인 계정으로 Azure 포털 toohello에 로그인 합니다.
2. Hello 자동화 계정 블레이드에서 선택 **실행 계정** hello 섹션 아래의 **계정 설정**합니다.  
3. 필요한 계정에 따라 **Azure 실행 계정** 또는 **Azure 클래식 실행 계정**을 선택합니다.  Hello 중 하나를 선택한 후 **추가 Azure 계정으로 실행** 또는 **Azure 클래식 실행 계정 추가** 블레이드 hello 개요 정보를 검토 한 후 클릭 나타나며 **만들기** 실행 계정 만들고와 tooproceed 합니다.  
4. Azure hello 실행 계정을 만들고, 하지만 아래 hello 진행률을 추적할 수 있습니다 **알림** hello에서 메뉴와 배너 라는 메시지가 표시 됩니다 hello 계정을 만드는 중입니다.  이 프로세스는 몇 분 toocomplete를 걸릴 수 있습니다.  

## <a name="create-run-as-account-using-powershell-script"></a>PowerShell 스크립트를 사용하여 실행 계정 만들기
이 PowerShell 스크립트는 구성을 따르고 hello에 대 한 지원이 포함 됩니다.

* 자체 서명된 인증서를 사용하여 실행 계정을 만듭니다.
* 자체 서명된 인증서를 사용하여 실행 계정 및 클래식 실행 계정을 만듭니다.
* 엔터프라이즈 인증서를 사용하여 실행 계정 및 클래식 실행 계정을 만듭니다.
* Hello Azure Government 클라우드에서에서 자체 서명 된 인증서를 사용 하 여 실행 계정 및 기존 실행 계정을 만듭니다.

선택한 hello 구성 옵션에 따라 hello 스크립트 hello 다음 항목을 만듭니다.

**실행 계정의 경우:**

* 만듭니다는 Azure AD 응용 프로그램 toobe 자체 서명 하거나 hello를 사용 하 여 내보낸 또는 엔터프라이즈 인증서 공개 키를 hello 응용 프로그램에 대 한 서비스 사용자 계정에 Azure AD를 만들고 할당 hello 후 현재에서 hello 계정에 대 한 참가자 역할 구독입니다. 이 설정은 tooOwner 또는 다른 역할을 변경할 수 있습니다. 자세한 내용은 [Azure Automation의 역할 기반 액세스 제어](automation-role-based-access-control.md)를 참조하세요.
* 명명 된 자동화 인증서 자산을 만듭니다 *AzureRunAsCertificate* hello 자동화 계정을 지정 합니다. hello 인증서 자산 hello Azure AD 응용 프로그램에서 사용 되는 hello 인증서 개인 키를 보유 합니다.
* 명명 된 자동화 연결 자산을 만듭니다 *AzureRunAsConnection* hello 자동화 계정을 지정 합니다. hello applicationId, tenantId, subscriptionId, 및 인증서 지문을 hello 연결 자산을 보유합니다.

**클래식 실행 계정의 경우:**

* 명명 된 자동화 인증서 자산을 만듭니다 *AzureClassicRunAsCertificate* hello 자동화 계정을 지정 합니다. hello 인증서 자산 hello 관리 인증서에 의해 사용 된 hello 인증서 개인 키를 보유 합니다.
* 명명 된 자동화 연결 자산을 만듭니다 *AzureClassicRunAsConnection* hello 자동화 계정을 지정 합니다. hello 연결 자산 hello 구독 이름, subscriptionId, 이름과 인증서 자산을 보유합니다.

>[!NOTE]
> Hello 스크립트를 실행 한 후 기본 계정으로 실행 계정 만들기에 대 한 옵션 중 하나를 선택 하면 업로드 hello 공용 인증서 (.cer 파일 이름 확장명) toohello 관리 저장 hello 구독에 대 한 해당 hello 자동화 계정에 만들어졌습니다.
> 

1. 컴퓨터에서 스크립트를 다음 hello를 저장 합니다. 이 예제에서는 hello 파일 이름으로 저장 *새로 RunAsAccount.ps1*합니다.

        #Requires -RunAsAdministrator
        Param (
        [Parameter(Mandatory=$true)]
        [String] $ResourceGroup,

        [Parameter(Mandatory=$true)]
        [String] $AutomationAccountName,

        [Parameter(Mandatory=$true)]
        [String] $ApplicationDisplayName,

        [Parameter(Mandatory=$true)]
        [String] $SubscriptionId,

        [Parameter(Mandatory=$true)]
        [Boolean] $CreateClassicRunAsAccount,

        [Parameter(Mandatory=$true)]
        [String] $SelfSignedCertPlainPassword,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$EnvironmentName="AzureCloud",

        [Parameter(Mandatory=$false)]
        [int] $SelfSignedCertNoOfMonthsUntilExpired = 12
        )

        function CreateSelfSignedCertificate([string] $keyVaultName, [string] $certificateName, [string] $selfSignedCertPlainPassword,
                                       [string] $certPath, [string] $certPathCer, [string] $selfSignedCertNoOfMonthsUntilExpired ) {
        $Cert = New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation cert:\LocalMachine\My `
            -KeyExportPolicy Exportable -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
            -NotAfter (Get-Date).AddMonths($selfSignedCertNoOfMonthsUntilExpired)

        $CertPassword = ConvertTo-SecureString $selfSignedCertPlainPassword -AsPlainText -Force
        Export-PfxCertificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPath -Password $CertPassword -Force | Write-Verbose
        Export-Certificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPathCer -Type CERT | Write-Verbose
        }

        function CreateServicePrincipal([System.Security.Cryptography.X509Certificates.X509Certificate2] $PfxCert, [string] $applicationDisplayName) {  
        $CurrentDate = Get-Date
        $keyValue = [System.Convert]::ToBase64String($PfxCert.GetRawCertData())
        $KeyId = (New-Guid).Guid

        $KeyCredential = New-Object  Microsoft.Azure.Commands.Resources.Models.ActiveDirectory.PSADKeyCredential
        $KeyCredential.StartDate = $CurrentDate
        $KeyCredential.EndDate = Get-Date $PfxCert.GetExpirationDateString()
        $KeyCredential.EndDate = $KeyCredential.EndDate.AddDays(-1)
        $KeyCredential.KeyId = $KeyId
        $KeyCredential.CertValue  = $keyValue

        # Use key credentials and create an Azure AD application
        $Application = New-AzureRmADApplication -DisplayName $ApplicationDisplayName -HomePage ("http://" + $applicationDisplayName) -IdentifierUris ("http://" + $KeyId) -KeyCredentials $KeyCredential
        $ServicePrincipal = New-AzureRMADServicePrincipal -ApplicationId $Application.ApplicationId
        $GetServicePrincipal = Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id

        # Sleep here for a few seconds tooallow hello service principal application toobecome active (ordinarily takes a few seconds)
        Sleep -s 15
        $NewRole = New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
        $Retries = 0;
        While ($NewRole -eq $null -and $Retries -le 6)
        {
            Sleep -s 10
            New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
            $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
            $Retries++;
        }
            return $Application.ApplicationId.ToString();
        }

        function CreateAutomationCertificateAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $certifcateAssetName,[string] $certPath, [string] $certPlainPassword, [Boolean] $Exportable) {
        $CertPassword = ConvertTo-SecureString $certPlainPassword -AsPlainText -Force   
        Remove-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $certifcateAssetName -ErrorAction SilentlyContinue
        New-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Path $certPath -Name $certifcateAssetName -Password $CertPassword -Exportable:$Exportable  | write-verbose
        }

        function CreateAutomationConnectionAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $connectionAssetName, [string] $connectionTypeName, [System.Collections.Hashtable] $connectionFieldValues ) {
        Remove-AzureRmAutomationConnection -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -Force -ErrorAction SilentlyContinue
        New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -ConnectionTypeName $connectionTypeName -ConnectionFieldValues $connectionFieldValues
        }

        Import-Module AzureRM.Profile
        Import-Module AzureRM.Resources

        $AzureRMProfileVersion= (Get-Module AzureRM.Profile).Version
        if (!(($AzureRMProfileVersion.Major -ge 3 -and $AzureRMProfileVersion.Minor -ge 0) -or ($AzureRMProfileVersion.Major -gt 3)))
        {
            Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
            return
        }

        Login-AzureRmAccount -Environment $EnvironmentName 
        $Subscription = Select-AzureRmSubscription -SubscriptionId $SubscriptionId

        # Create a Run As account by using a service principal
        $CertifcateAssetName = "AzureRunAsCertificate"
        $ConnectionAssetName = "AzureRunAsConnection"
        $ConnectionTypeName = "AzureServicePrincipal"

        if ($EnterpriseCertPathForRunAsAccount -and $EnterpriseCertPlainPasswordForRunAsAccount) {
        $PfxCertPathForRunAsAccount = $EnterpriseCertPathForRunAsAccount
        $PfxCertPlainPasswordForRunAsAccount = $EnterpriseCertPlainPasswordForRunAsAccount
        } else {
           $CertificateName = $AutomationAccountName+$CertifcateAssetName
           $PfxCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".pfx")
           $PfxCertPlainPasswordForRunAsAccount = $SelfSignedCertPlainPassword
           $CerCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".cer")
           CreateSelfSignedCertificate $KeyVaultName $CertificateName $PfxCertPlainPasswordForRunAsAccount $PfxCertPathForRunAsAccount $CerCertPathForRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create a service principal
        $PfxCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($PfxCertPathForRunAsAccount, $PfxCertPlainPasswordForRunAsAccount)
        $ApplicationId=CreateServicePrincipal $PfxCert $ApplicationDisplayName

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate hello ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
             # Create a Run As account by using a service principal
             $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
             $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
             $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
             $UploadMessage = "Please upload hello .cer format of #CERT# toohello Management store by following hello steps below." + [Environment]::NewLine +
                     "Log in toohello Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                     "Then click Upload and upload hello .cer format of #CERT#"

              if ($EnterpriseCertPathForClassicRunAsAccount -and $EnterpriseCertPlainPasswordForClassicRunAsAccount ) {
              $PfxCertPathForClassicRunAsAccount = $EnterpriseCertPathForClassicRunAsAccount
              $PfxCertPlainPasswordForClassicRunAsAccount = $EnterpriseCertPlainPasswordForClassicRunAsAccount
              $UploadMessage = $UploadMessage.Replace("#CERT#", $PfxCertPathForClassicRunAsAccount)
        } else {
              $ClassicRunAsAccountCertificateName = $AutomationAccountName+$ClassicRunAsAccountCertifcateAssetName
              $PfxCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".pfx")
              $PfxCertPlainPasswordForClassicRunAsAccount = $SelfSignedCertPlainPassword
              $CerCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".cer")
              $UploadMessage = $UploadMessage.Replace("#CERT#", $CerCertPathForClassicRunAsAccount)
              CreateSelfSignedCertificate $KeyVaultName $ClassicRunAsAccountCertificateName $PfxCertPlainPasswordForClassicRunAsAccount $PfxCertPathForClassicRunAsAccount $CerCertPathForClassicRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate hello ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.Name
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. 사용자 컴퓨터에서 시작 **Windows PowerShell** hello에서 **시작** 관리자 권한으로 화면입니다.
3. Hello에서 높은 명령줄 셸 1 단계에서 만든 hello 스크립트가 들어 있는 이동 toohello 폴더.  
4. 필요한 hello 구성에 대 한 hello 매개 변수 값을 사용 하 여 hello 스크립트를 실행 합니다.

    **자체 서명된 인증서를 사용하여 실행 계정 만들기**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    **자체 서명된 인증서를 사용하여 실행 계정 및 클래식 실행 계정 만들기**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    **엔터프라이즈 인증서를 사용하여 실행 계정 및 클래식 실행 계정 만들기**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    **Hello Azure Government 클라우드에서에서 자체 서명 된 인증서를 사용 하 여 실행 계정 및 클래식 계정으로 실행 계정 만들기**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > Hello 스크립트 실행 된 후 Azure 사용한 메시지 표시 tooauthenticate 됩니다. Hello 구독 관리자 역할의 구성원 및 hello 구독의 공동 관리자 인 계정으로 로그인 합니다.
    >
    >

Hello 스크립트 성공적으로 실행 된 후에 hello 다음 note:
* Hello 스크립트 만들고 hello 사용자 프로필 아래에 임시 파일 폴더 toohello 저장 자체 서명 된 공용 인증서 (.cer 파일)를 사용 하 여 기존 실행 계정을 만든 경우 *%USERPROFILE%\AppData\Local\Temp*, tooexecute hello PowerShell 세션을 사용 합니다.
* 엔터프라이즈 공용 인증서(.cer 파일)를 사용하여 클래식 실행 계정을 만든 경우 이 인증서를 사용합니다. 에 대 한 hello 지침 [관리 API 인증서 toohello Azure 클래식 포털을 업로드](../azure-api-management-certs.md), hello를 사용 하 여 클래식 배포 리소스와 hello 자격 증명 구성의 유효성을 검사 하 [샘플 코드 Azure 클래식 배포 리소스와 tooauthenticate](automation-verify-runas-authentication.md#classic-run-as-authentication)합니다. 
* 작업을 수행한 경우 *하지* 클래식 실행 계정을 만들고 리소스 관리자 리소스를 사용 하 여 인증 hello를 사용 하 여 hello 자격 증명 구성 유효성 검사 [서비스 관리를 사용 하 여 인증에 대 한 코드 샘플 리소스](automation-verify-runas-authentication.md#automation-run-as-authentication)합니다.

## <a name="next-steps"></a>다음 단계
* 서비스 사용자에 대 한 자세한 내용은 참조 너무[응용 프로그램 개체 및 서비스 주체 개체](../active-directory/active-directory-application-objects.md)합니다.
* 인증서 및 Azure 서비스에 대 한 자세한 내용은 참조 너무[Azure 클라우드 서비스에 대 한 인증서 개요](../cloud-services/cloud-services-certs-create.md)합니다.
