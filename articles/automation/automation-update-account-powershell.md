---
title: "Azure 자동화 실행 계정 powershell aaaCreate | Microsoft Docs"
description: "이 문서에서는 어떻게 tooupgrade 자동화 계정으로 실행 하는 PowerShell toocreate hello로 계정 hello 포털에서 초기 작성 하는 동안이 단계를 수행 하지 않은 경우를 설명 합니다."
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
ms.date: 04/14/2017
ms.author: magoedte
ms.openlocfilehash: 1049601321d2bc1e5f9d982f622788f8e4e4d797
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="update-automation-run-as-account-using-powershell"></a><span data-ttu-id="ede35-103">PowerShell을 사용하여 Automation 실행 계정 업데이트</span><span class="sxs-lookup"><span data-stu-id="ede35-103">Update Automation Run As account using PowerShell</span></span>
<span data-ttu-id="ede35-104">경우 기존 자동화 계정을 PowerShell tooupdate을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-104">You can use PowerShell tooupdate your existing Automation account if:</span></span>

* <span data-ttu-id="ede35-105">자동화 계정을 만들지만 toocreate hello 계정으로 실행을 거부 합니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-105">You create an Automation account but decline toocreate hello Run As account.</span></span>
* <span data-ttu-id="ede35-106">자동화 계정 toomanage 리소스 관리자 리소스를 이미 사용 중이 고 tooupdate hello 계정 tooinclude hello 실행 계정을 runbook 인증에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-106">You already use an Automation account toomanage Resource Manager resources and you want tooupdate hello account tooinclude hello Run As account for runbook authentication.</span></span>
* <span data-ttu-id="ede35-107">자동화 계정 toomanage 클래식 리소스를 이미 사용 중이 고 tooupdate 것 toouse hello 클래식 실행 계정 대신 새 계정을 만들고 runbook과 자산 tooit 마이그레이션.</span><span class="sxs-lookup"><span data-stu-id="ede35-107">You already use an Automation account toomanage classic resources and you want tooupdate it toouse hello Classic Run As account instead of creating a new account and migrating your runbooks and assets tooit.</span></span>   
* <span data-ttu-id="ede35-108">Toocreate 실행 하 고 기본 실행 계정을 사용 하 여 원하는 엔터프라이즈 인증 기관 (CA)에서 발급 한 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-108">You want toocreate a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ede35-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ede35-109">Prerequisites</span></span>

* <span data-ttu-id="ede35-110">Azure 리소스 관리자 모듈 2.01 이상 hello 스크립트를 Windows 10 및 Windows Server 2016에 대해서만 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-110">hello script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 2.01 and later.</span></span> <span data-ttu-id="ede35-111">이전 버전의 Windows에서는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-111">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="ede35-112">Azure PowerShell 1.0 이상</span><span class="sxs-lookup"><span data-stu-id="ede35-112">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="ede35-113">PowerShell 1.0 hello 릴리스에 대 한 자세한 내용은 참조 하십시오. [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-113">For information about hello PowerShell 1.0 release, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="ede35-114">Hello에 대 한 hello 값으로 참조 하는 자동화 계정을 *– AutomationAccountName* 및 *-ApplicationDisplayName* hello PowerShell 스크립트 뒤에 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-114">An Automation account, which is referenced as hello value for hello *–AutomationAccountName* and *-ApplicationDisplayName* parameters in hello following PowerShell script.</span></span>

<span data-ttu-id="ede35-115">tooget hello에 대 한 값 *SubscriptionID*, *ResourceGroup*, 및 *AutomationAccountName*, hello 스크립트에 대 한 필수 매개 변수는, 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-115">tooget hello values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for hello scripts, do hello following:</span></span>
1. <span data-ttu-id="ede35-116">Hello Azure 포털에서 hello에서 자동화 계정을 선택 **자동화 계정** 블레이드에서 다음을 선택 하 고 **모든 설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-116">In hello Azure portal, select your Automation account on hello **Automation account** blade, and then select **All settings**.</span></span> 
2. <span data-ttu-id="ede35-117">Hello에 **모든 설정을** 블레이드 아래 **계정 설정**선택, **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-117">On hello **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="ede35-118">Hello에 hello 값을 기록 **속성** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-118">Note hello values on hello **Properties** blade.</span></span>

![hello 자동화 계정 "속성" 블레이드](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

## <a name="create-run-as-account-powershell-script"></a><span data-ttu-id="ede35-120">실행 계정 PowerShell 스크립트 만들기</span><span class="sxs-lookup"><span data-stu-id="ede35-120">Create Run As Account PowerShell script</span></span>
<span data-ttu-id="ede35-121">이 PowerShell 스크립트는 구성을 따르고 hello에 대 한 지원이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-121">This PowerShell script includes support for hello following configurations:</span></span>

* <span data-ttu-id="ede35-122">자체 서명된 인증서를 사용하여 실행 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-122">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="ede35-123">자체 서명된 인증서를 사용하여 실행 계정 및 클래식 실행 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-123">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="ede35-124">엔터프라이즈 인증서를 사용하여 실행 계정 및 클래식 실행 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-124">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="ede35-125">Hello Azure Government 클라우드에서에서 자체 서명 된 인증서를 사용 하 여 실행 계정 및 기존 실행 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-125">Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud.</span></span>

<span data-ttu-id="ede35-126">선택한 hello 구성 옵션에 따라 hello 스크립트 hello 다음 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-126">Depending on hello configuration option you select, hello script creates hello following items.</span></span>

<span data-ttu-id="ede35-127">**실행 계정의 경우:**</span><span class="sxs-lookup"><span data-stu-id="ede35-127">**For Run As accounts:**</span></span>

* <span data-ttu-id="ede35-128">만듭니다는 Azure AD 응용 프로그램 toobe 자체 서명 하거나 hello를 사용 하 여 내보낸 또는 엔터프라이즈 인증서 공개 키를 hello 응용 프로그램에 대 한 서비스 사용자 계정에 Azure AD를 만들고 할당 hello 후 현재에서 hello 계정에 대 한 참가자 역할 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-128">Creates an Azure AD application toobe exported with either hello self-signed or enterprise certificate public key, creates a service principal account for hello application in Azure AD, and assigns hello Contributor role for hello account in your current subscription.</span></span> <span data-ttu-id="ede35-129">이 설정은 tooOwner 또는 다른 역할을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-129">You can change this setting tooOwner or any other role.</span></span> <span data-ttu-id="ede35-130">자세한 내용은 [Azure Automation의 역할 기반 액세스 제어](automation-role-based-access-control.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ede35-130">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="ede35-131">명명 된 자동화 인증서 자산을 만듭니다 *AzureRunAsCertificate* hello 자동화 계정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-131">Creates an Automation certificate asset named *AzureRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="ede35-132">hello 인증서 자산 hello Azure AD 응용 프로그램에서 사용 되는 hello 인증서 개인 키를 보유 합니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-132">hello certificate asset holds hello certificate private key that's used by hello Azure AD application.</span></span>
* <span data-ttu-id="ede35-133">명명 된 자동화 연결 자산을 만듭니다 *AzureRunAsConnection* hello 자동화 계정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-133">Creates an Automation connection asset named *AzureRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="ede35-134">hello applicationId, tenantId, subscriptionId, 및 인증서 지문을 hello 연결 자산을 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-134">hello connection asset holds hello applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="ede35-135">**클래식 실행 계정의 경우:**</span><span class="sxs-lookup"><span data-stu-id="ede35-135">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="ede35-136">명명 된 자동화 인증서 자산을 만듭니다 *AzureClassicRunAsCertificate* hello 자동화 계정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-136">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="ede35-137">hello 인증서 자산 hello 관리 인증서에 의해 사용 된 hello 인증서 개인 키를 보유 합니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-137">hello certificate asset holds hello certificate private key used by hello management certificate.</span></span>
* <span data-ttu-id="ede35-138">명명 된 자동화 연결 자산을 만듭니다 *AzureClassicRunAsConnection* hello 자동화 계정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-138">Creates an Automation connection asset named *AzureClassicRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="ede35-139">hello 연결 자산 hello 구독 이름, subscriptionId, 이름과 인증서 자산을 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-139">hello connection asset holds hello subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="ede35-140">Hello 스크립트를 실행 한 후 기본 계정으로 실행 계정 만들기에 대 한 옵션 중 하나를 선택 하면 업로드 hello 공용 인증서 (.cer 파일 이름 확장명) toohello 관리 저장 hello 구독에 대 한 해당 hello 자동화 계정에 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-140">If you select either option for creating a Classic Run As account, after hello script is executed, upload hello public certificate (.cer file name extension) toohello management store for hello subscription that hello Automation account was created in.</span></span>
> 

1. <span data-ttu-id="ede35-141">컴퓨터에서 스크립트를 다음 hello를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-141">Save hello following script on your computer.</span></span> <span data-ttu-id="ede35-142">이 예제에서는 hello 파일 이름으로 저장 *새로 RunAsAccount.ps1*합니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-142">In this example, save it with hello filename *New-RunAsAccount.ps1*.</span></span>

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
        $KeyCredential.EndDate= [DateTime]$PfxCert.GetExpirationDateString()
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
        if (!(($AzureRMProfileVersion.Major -ge 2 -and $AzureRMProfileVersion.Minor -ge 1) -or ($AzureRMProfileVersion.Major -gt 2)))
        {
           Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
           return
        }

        Login-AzureRmAccount -EnvironmentName $EnvironmentName
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
        $SubscriptionName = $subscription.Subscription.SubscriptionName
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="ede35-143">사용자 컴퓨터에서 시작 **Windows PowerShell** hello에서 **시작** 관리자 권한으로 화면입니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-143">On your computer, start **Windows PowerShell** from hello **Start** screen with elevated user rights.</span></span>
3. <span data-ttu-id="ede35-144">Hello에서 높은 명령줄 셸 1 단계에서 만든 hello 스크립트가 들어 있는 이동 toohello 폴더.</span><span class="sxs-lookup"><span data-stu-id="ede35-144">From hello elevated command-line shell, go toohello folder that contains hello script you created in step 1.</span></span>  
4. <span data-ttu-id="ede35-145">필요한 hello 구성에 대 한 hello 매개 변수 값을 사용 하 여 hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-145">Execute hello script by using hello parameter values for hello configuration you require.</span></span>

    <span data-ttu-id="ede35-146">**자체 서명된 인증서를 사용하여 실행 계정 만들기**</span><span class="sxs-lookup"><span data-stu-id="ede35-146">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="ede35-147">**자체 서명된 인증서를 사용하여 실행 계정 및 클래식 실행 계정 만들기**</span><span class="sxs-lookup"><span data-stu-id="ede35-147">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="ede35-148">**엔터프라이즈 인증서를 사용하여 실행 계정 및 클래식 실행 계정 만들기**</span><span class="sxs-lookup"><span data-stu-id="ede35-148">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="ede35-149">**Hello Azure Government 클라우드에서에서 자체 서명 된 인증서를 사용 하 여 실행 계정 및 클래식 계정으로 실행 계정 만들기**</span><span class="sxs-lookup"><span data-stu-id="ede35-149">**Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="ede35-150">Hello 스크립트 실행 된 후 Azure 사용한 메시지 표시 tooauthenticate 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-150">After hello script has executed, you will be prompted tooauthenticate with Azure.</span></span> <span data-ttu-id="ede35-151">Hello 구독 관리자 역할의 구성원 및 hello 구독의 공동 관리자 인 계정으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-151">Sign in with an account that is a member of hello subscription administrators role and co-administrator of hello subscription.</span></span>
    >
    >

<span data-ttu-id="ede35-152">Hello 스크립트 성공적으로 실행 된 후에 hello 다음 note:</span><span class="sxs-lookup"><span data-stu-id="ede35-152">After hello script has executed successfully, note hello following:</span></span>
* <span data-ttu-id="ede35-153">Hello 스크립트 만들고 hello 사용자 프로필 아래에 임시 파일 폴더 toohello 저장 자체 서명 된 공용 인증서 (.cer 파일)를 사용 하 여 기존 실행 계정을 만든 경우 *%USERPROFILE%\AppData\Local\Temp*, tooexecute hello PowerShell 세션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-153">If you created a Classic Run As account with a self-signed public certificate (.cer file), hello script creates and saves it toohello temporary files folder on your computer under hello user profile *%USERPROFILE%\AppData\Local\Temp*, which you used tooexecute hello PowerShell session.</span></span>
* <span data-ttu-id="ede35-154">엔터프라이즈 공용 인증서(.cer 파일)를 사용하여 클래식 실행 계정을 만든 경우 이 인증서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-154">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="ede35-155">에 대 한 hello 지침 [관리 API 인증서 toohello Azure 클래식 포털을 업로드](../azure-api-management-certs.md), hello를 사용 하 여 클래식 배포 리소스와 hello 자격 증명 구성의 유효성을 검사 하 [샘플 코드 Azure 클래식 배포 리소스와 tooauthenticate](automation-verify-runas-authentication.md#classic-run-as-authentication)합니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-155">Follow hello instructions for [uploading a management API certificate toohello Azure classic portal](../azure-api-management-certs.md), and then validate hello credential configuration with classic deployment resources by using hello [sample code tooauthenticate with Azure Classic Deployment Resources](automation-verify-runas-authentication.md#classic-run-as-authentication).</span></span> 
* <span data-ttu-id="ede35-156">작업을 수행한 경우 *하지* 클래식 실행 계정을 만들고 리소스 관리자 리소스를 사용 하 여 인증 hello를 사용 하 여 hello 자격 증명 구성 유효성 검사 [서비스 관리를 사용 하 여 인증에 대 한 코드 샘플 리소스](automation-verify-runas-authentication.md#automation-run-as-authentication)합니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-156">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate hello credential configuration by using hello [sample code for authenticating with Service Management resources](automation-verify-runas-authentication.md#automation-run-as-authentication).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ede35-157">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ede35-157">Next steps</span></span>
* <span data-ttu-id="ede35-158">서비스 사용자에 대 한 자세한 내용은 참조 너무[응용 프로그램 개체 및 서비스 주체 개체](../active-directory/active-directory-application-objects.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-158">For more information about Service Principals, refer too[Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="ede35-159">인증서 및 Azure 서비스에 대 한 자세한 내용은 참조 너무[Azure 클라우드 서비스에 대 한 인증서 개요](../cloud-services/cloud-services-certs-create.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ede35-159">For more information about certificates and Azure services, refer too[Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>
