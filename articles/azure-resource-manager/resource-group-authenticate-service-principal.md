---
title: "PowerShell과 함께 Azure 응용 프로그램에 대 한 aaaCreate id | Microsoft Docs"
description: "Azure PowerShell toocreate toouse Azure Active Directory 응용 프로그램 및 서비스 사용자 및 역할 기반 액세스를 통해 tooresources 액세스용 부여 제어 하는 방법에 대해 설명 합니다. 표시 방법을 tooauthenticate 응용 프로그램 암호 또는 인증서를 사용 합니다."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: d2caf121-9fbe-4f00-bf9d-8f3d1f00a6ff
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: c534360799b590054a051e4426e5e27dccb559b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-powershell-toocreate-a-service-principal-tooaccess-resources"></a>Azure PowerShell toocreate 서비스 보안 주체 tooaccess 리소스 사용

응용 프로그램 또는 스크립트를 tooaccess 리소스가 필요한 경우 hello 앱에 대 한 id를 설정할 수 있으며 자체 자격 증명으로 hello 앱을 인증 합니다. 이 ID를 서비스 주체라고 합니다. 이 접근 방법을 사용하면 다음을 수행할 수 있습니다.

* 권한을 자신만 사용 권한을 것과 다른 toohello 응용 프로그램 id를 할당 합니다. 일반적으로 이러한 권한은 제한 된 tooexactly 어떤 hello 앱 toodo 필요 합니다.
* 무인 스크립트를 실행할 때 인증을 위해 인증서를 사용합니다.

이 항목에서는 toouse [Azure PowerShell](/powershell/azure/overview) tooset 자체 자격 증명 및 id에서 응용 프로그램 toorun 프로그램에 필요한 모든 항목을 합니다.

## <a name="required-permissions"></a>필요한 사용 권한
toocomplete이이 항목에서는 Azure Active Directory와 Azure 구독에서 충분 한 권한이 있어야 합니다. 특히 수 toocreate hello Azure Active Directory에에서는 앱이 될 하 고 hello 서비스 보안 주체 tooa 역할을 할당 해야 합니다. 

hello 가장 쉬운 방법은 toocheck hello 포털을 통해이 계정을 적절 한 사용 권한이 있는지 여부. [필요한 사용 권한 확인](resource-group-create-service-principal-portal.md#required-permissions)을 참조하세요.

이제 tooa 섹션에 인증 하기 위해 계속 수행 합니다.

* [암호](#create-service-principal-with-password)
* [자체 서명된 인증서](#create-service-principal-with-self-signed-certificate)
* [인증 기관의 인증서](#create-service-principal-with-certificate-from-certificate-authority)

## <a name="powershell-commands"></a>PowerShell 명령

사용 서비스 사용자를 tooset, 합니다.

| 명령 | 설명 |
| ------- | ----------- | 
| [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | Azure Active Directory 서비스 주체 만들기 |
| [New-AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment) | 할당 hello RBAC 역할 toohello 지정한 보안 주체가 지정 된, hello에 범위를 지정 합니다. |


## <a name="create-service-principal-with-password"></a>암호를 사용하여 서비스 주체 만들기

toocreate 구독에 대 한 hello 참가자 역할 인 서비스 사용자를 사용 합니다. 

```powershell
Login-AzureRmAccount
$sp = New-AzureRmADServicePrincipal -DisplayName exampleapp -Password "{provide-password}"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

hello 예제는 전체 Azure Active Directory에서 hello 제공 하는 서비스 새 주 toopropagate 약간의 시간이 tooallow 20 초 동안 대기합니다. 스크립트는 충분 한 시간 동안 대기 하지 않고 표시 한다는 오류: "PrincipalNotFound: 보안 주체 {id} hello 디렉터리에 존재 하지 않습니다."

hello 다음 스크립트 toospecify hello 기본 구독 이외의 범위 있으며 오류가 발생할 경우 재시도 hello 역할 할당:

```powershell
Param (

 # Use tooset scope tooresource group. If no value is provided, scope is set toosubscription.
 [Parameter(Mandatory=$false)]
 [String] $ResourceGroup,

 # Use tooset subscription. If no value is provided, default subscription is used. 
 [Parameter(Mandatory=$false)]
 [String] $SubscriptionId,

 [Parameter(Mandatory=$true)]
 [String] $ApplicationDisplayName,

 [Parameter(Mandatory=$true)]
 [String] $Password
)

 Login-AzureRmAccount
 Import-Module AzureRM.Resources

 if ($SubscriptionId -eq "") 
 {
    $SubscriptionId = (Get-AzureRmContext).Subscription.Id
 }
 else
 {
    Set-AzureRmContext -SubscriptionId $SubscriptionId
 }

 if ($ResourceGroup -eq "")
 {
    $Scope = "/subscriptions/" + $SubscriptionId
 }
 else
 {
    $Scope = (Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop).ResourceId
 }

 
 # Create Service Principal for hello AD app
 $ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -Password $Password
 Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 

 $NewRole = $null
 $Retries = 0;
 While ($NewRole -eq $null -and $Retries -le 6)
 {
    # Sleep here for a few seconds tooallow hello service principal application toobecome active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
```

Hello 스크립트에 대 한 몇 가지 항목 toonote:

* toogrant hello identity 액세스 toohello 기본 구독 않아도 tooprovide ResourceGroup 또는 SubscriptionId 매개 변수입니다.
* Toolimit hello 범위 hello 역할 할당 tooa 리소스 그룹의 경우에 hello ResourceGroup 매개 변수를 지정 합니다.
*  이 예제에서는 hello 서비스 보안 주체 toohello 참가자 역할을 추가합니다. 다른 역할에 대해서는 [RBAC: 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md)을 참조하세요.
* hello 스크립트는 전체 Azure Active Directory에서 hello 제공 하는 서비스 새 주 toopropagate 약간의 시간이 tooallow 15 초 동안 대기합니다. 스크립트는 충분 한 시간 동안 대기 하지 않고 표시 한다는 오류: "PrincipalNotFound: 보안 주체 {id} hello 디렉터리에 존재 하지 않습니다."
* Toogrant hello 서비스 보안 주체 액세스 toomore 구독 또는 리소스 그룹을 해야 하는 경우 실행 hello `New-AzureRMRoleAssignment` 다양 한 범위를 사용 하 여 다시 cmdlet.


### <a name="provide-credentials-through-powershell"></a>PowerShell을 통해 자격 증명 제공
이제, hello 응용 프로그램 tooperform 작업으로 toolog에 필요 합니다. Hello 사용자 이름에 대 한 hello를 사용 하 여 `ApplicationId` hello 응용 프로그램에 대해 만든 합니다. Hello 암호에 대 한 hello hello 계정을 만들 때 지정 하나를 사용 합니다. 

```powershell   
$creds = Get-Credential
Login-AzureRmAccount -Credential $creds -ServicePrincipal -TenantId {tenant-id}
```

테 넌 트 ID hello/소문자를 구분 하지 않으므로 스크립트에서 직접 포함할 수 있습니다. Tooretrieve hello 테 넌 트 ID, 필요한 경우 사용 합니다.

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

## <a name="create-service-principal-with-self-signed-certificate"></a>자체 서명된 인증서를 사용하여 서비스 주체 만들기

toocreate 자체 서명 된 인증서와 구독에 대 한 hello 참가자 역할 서비스 사용자를 사용 합니다. 

```powershell
Login-AzureRmAccount
$cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=exampleappScriptCert" -KeySpec KeyExchange
$keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())

$sp = New-AzureRMADServicePrincipal -DisplayName exampleapp -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

hello 예제는 전체 Azure Active Directory에서 hello 제공 하는 서비스 새 주 toopropagate 약간의 시간이 tooallow 20 초 동안 대기합니다. 스크립트는 충분 한 시간 동안 대기 하지 않고 표시 한다는 오류: "PrincipalNotFound: 보안 주체 {id} hello 디렉터리에 존재 하지 않습니다."

hello 다음 스크립트 toospecify hello 기본 구독 이외의 범위 있으며 오류가 발생할 경우 재시도 hello 역할 할당 합니다. Windows 10 또는 Windows Server 2016에서 Azure PowerShell 2.0이 있어야 합니다.

```powershell
Param (

 # Use tooset scope tooresource group. If no value is provided, scope is set toosubscription.
 [Parameter(Mandatory=$false)]
 [String] $ResourceGroup,

 # Use tooset subscription. If no value is provided, default subscription is used. 
 [Parameter(Mandatory=$false)]
 [String] $SubscriptionId,

 [Parameter(Mandatory=$true)]
 [String] $ApplicationDisplayName
 )

 Login-AzureRmAccount
 Import-Module AzureRM.Resources

 if ($SubscriptionId -eq "") 
 {
    $SubscriptionId = (Get-AzureRmContext).Subscription.Id
 }
 else
 {
    Set-AzureRmContext -SubscriptionId $SubscriptionId
 }

 if ($ResourceGroup -eq "")
 {
    $Scope = "/subscriptions/" + $SubscriptionId
 }
 else
 {
    $Scope = (Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop).ResourceId
 }

 $cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=exampleappScriptCert" -KeySpec KeyExchange
 $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())

 $ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
 Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 

 $NewRole = $null
 $Retries = 0;
 While ($NewRole -eq $null -and $Retries -le 6)
 {
    # Sleep here for a few seconds tooallow hello service principal application toobecome active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
```

Hello 스크립트에 대 한 몇 가지 항목 toonote:

* toogrant hello identity 액세스 toohello 기본 구독 않아도 tooprovide ResourceGroup 또는 SubscriptionId 매개 변수입니다.
* Toolimit hello 범위 hello 역할 할당 tooa 리소스 그룹의 경우에 hello ResourceGroup 매개 변수를 지정 합니다.
* 이 예제에서는 hello 서비스 보안 주체 toohello 참가자 역할을 추가합니다. 다른 역할에 대해서는 [RBAC: 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md)을 참조하세요.
* hello 스크립트는 전체 Azure Active Directory에서 hello 제공 하는 서비스 새 주 toopropagate 약간의 시간이 tooallow 15 초 동안 대기합니다. 스크립트는 충분 한 시간 동안 대기 하지 않고 표시 한다는 오류: "PrincipalNotFound: 보안 주체 {id} hello 디렉터리에 존재 하지 않습니다."
* Toogrant hello 서비스 보안 주체 액세스 toomore 구독 또는 리소스 그룹을 해야 하는 경우 실행 hello `New-AzureRMRoleAssignment` 다양 한 범위를 사용 하 여 다시 cmdlet.

경우 있습니다 **Windows 10 또는 Windows Server 2016 Technical Preview 없는**, toodownload hello 해야 [자체 서명 된 인증서 생성기](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) Microsoft 스크립트 센터에서. 콘텐츠를 추출 하 고 필요한 hello cmdlet을 가져옵니다.

```powershell  
# Only run if you could not use New-SelfSignedCertificate
Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
```
  
Hello 스크립트에서 다음 두 줄 toogenerate hello 인증서 hello를 대체 합니다.
  
```powershell
New-SelfSignedCertificateEx  -StoreLocation CurrentUser -StoreName My -Subject "CN=exampleapp" -KeySpec "Exchange" -FriendlyName "exampleapp"
$cert = Get-ChildItem -path Cert:\CurrentUser\my | where {$PSitem.Subject -eq 'CN=exampleapp' }
```

### <a name="provide-certificate-through-automated-powershell-script"></a>자동화된 PowerShell 스크립트를 통해 인증서 제공
서비스 사용자로 로그인 할 때마다 AD 앱에 대 한 hello 디렉터리의 tooprovide hello 테 넌 트 id가 필요 합니다. 테넌트는 Azure Active Directory의 인스턴스입니다. 구독이 하나만 있는 경우 다음을 사용할 수 있습니다.

```powershell
Param (
 
 [Parameter(Mandatory=$true)]
 [String] $CertSubject,
 
 [Parameter(Mandatory=$true)]
 [String] $ApplicationId,

 [Parameter(Mandatory=$true)]
 [String] $TenantId
 )

 $Thumbprint = (Get-ChildItem cert:\CurrentUser\My\ | Where-Object {$_.Subject -match $CertSubject }).Thumbprint
 Login-AzureRmAccount -ServicePrincipal -CertificateThumbprint $Thumbprint -ApplicationId $ApplicationId -TenantId $TenantId
```

ID 및 테 넌 트 ID hello 응용 프로그램/소문자를 구분 하지 않으므로 스크립트에서 직접 포함할 수 있습니다. Tooretrieve hello 테 넌 트 ID, 필요한 경우 사용 합니다.

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

Tooretrieve hello 응용 프로그램 ID, 필요한 경우 사용 합니다.

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="create-service-principal-with-certificate-from-certificate-authority"></a>인증 기관의 인증서를 사용하여 서비스 주체 만들기
인증 기관 toocreate 서비스 사용자를 사용 하 여 hello 다음 스크립트에서 발급 한 인증서 toouse:

```powershell
Param (
 [Parameter(Mandatory=$true)]
 [String] $ApplicationDisplayName,

 [Parameter(Mandatory=$true)]
 [String] $SubscriptionId,

 [Parameter(Mandatory=$true)]
 [String] $CertPath,

 [Parameter(Mandatory=$true)]
 [String] $CertPlainPassword
 )

 Login-AzureRmAccount
 Import-Module AzureRM.Resources
 Set-AzureRmContext -SubscriptionId $SubscriptionId

 $KeyId = (New-Guid).Guid
 $CertPassword = ConvertTo-SecureString $CertPlainPassword -AsPlainText -Force

 $PFXCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($CertPath, $CertPassword)
 $KeyValue = [System.Convert]::ToBase64String($PFXCert.GetRawCertData())

 $KeyCredential = New-Object  Microsoft.Azure.Commands.Resources.Models.ActiveDirectory.PSADKeyCredential
 $KeyCredential.StartDate = $PFXCert.NotBefore
 $KeyCredential.EndDate= $PFXCert.NotAfter
 $KeyCredential.KeyId = $KeyId
 $KeyCredential.CertValue = $KeyValue

 $ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -KeyCredentials $keyCredential
 Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 

 $NewRole = $null
 $Retries = 0;
 While ($NewRole -eq $null -and $Retries -le 6)
 {
    # Sleep here for a few seconds tooallow hello service principal application toobecome active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
 
 $NewRole
```

Hello 스크립트에 대 한 몇 가지 항목 toonote:

* 액세스 범위 지정 된 toohello 구독입니다.
* 이 예제에서는 hello 서비스 보안 주체 toohello 참가자 역할을 추가합니다. 다른 역할에 대해서는 [RBAC: 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md)을 참조하세요.
* hello 스크립트는 전체 Azure Active Directory에서 hello 제공 하는 서비스 새 주 toopropagate 약간의 시간이 tooallow 15 초 동안 대기합니다. 스크립트는 충분 한 시간 동안 대기 하지 않고 표시 한다는 오류: "PrincipalNotFound: 보안 주체 {id} hello 디렉터리에 존재 하지 않습니다."
* Toogrant hello 서비스 보안 주체 액세스 toomore 구독 또는 리소스 그룹을 해야 하는 경우 실행 hello `New-AzureRMRoleAssignment` 다양 한 범위를 사용 하 여 다시 cmdlet.

### <a name="provide-certificate-through-automated-powershell-script"></a>자동화된 PowerShell 스크립트를 통해 인증서 제공
서비스 사용자로 로그인 할 때마다 AD 앱에 대 한 hello 디렉터리의 tooprovide hello 테 넌 트 id가 필요 합니다. 테넌트는 Azure Active Directory의 인스턴스입니다.

```powershell
Param (
 
 [Parameter(Mandatory=$true)]
 [String] $CertPath,

 [Parameter(Mandatory=$true)]
 [String] $CertPlainPassword,
 
 [Parameter(Mandatory=$true)]
 [String] $ApplicationId,

 [Parameter(Mandatory=$true)]
 [String] $TenantId
 )

 $CertPassword = ConvertTo-SecureString $CertPlainPassword -AsPlainText -Force
 $PFXCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($CertPath, $CertPassword)
 $Thumbprint = $PFXCert.Thumbprint

 Login-AzureRmAccount -ServicePrincipal -CertificateThumbprint $Thumbprint -ApplicationId $ApplicationId -TenantId $TenantId
```

ID 및 테 넌 트 ID hello 응용 프로그램/소문자를 구분 하지 않으므로 스크립트에서 직접 포함할 수 있습니다. Tooretrieve hello 테 넌 트 ID, 필요한 경우 사용 합니다.

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

Tooretrieve hello 응용 프로그램 ID, 필요한 경우 사용 합니다.

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="change-credentials"></a>자격 증명 변경

hello를 사용 하는 보안 또는 자격 증명 만료 때문에 AD 응용 프로그램에 대 한 toochange hello 자격 [제거 AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) 및 [새로 AzureRmADAppCredential](/powershell/module/azurerm.resources/new-azurermadappcredential) cmdlet.

tooremove 응용 프로그램에 대 한 모든 hello 자격 증명을 사용 합니다.

```powershell
Remove-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -All
```

tooadd 암호를 사용 합니다.

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -Password p@ssword!
```

이 항목에 표시 된 대로 tooadd 인증서 값 자체 서명 된 인증서를 만듭니다. 그 후 다음을 사용합니다.

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
```

## <a name="save-access-token-toosimplify-log-in"></a>액세스 토큰 toosimplify 로그인 저장
tooavoid 제공 hello 서비스 사용자 자격 증명에 toolog 해야 할 때마다 hello 액세스 토큰을 저장할 수 있습니다.

이후 세션에서 toouse hello 현재 액세스 토큰이 hello 프로필을 저장 합니다.
   
```powershell
Save-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```
   
Hello 프로필 열고 해당 내용을 확인 합니다. 액세스 토큰을 포함하는지 확인합니다. 수동으로 다시 로그인을 대신 단순히 hello 프로필을 로드 합니다.
   
```powershell
Select-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```

> [!NOTE]
> 저장된 된 프로필을 사용 하 여만 작동에 대 한 hello 토큰은 유효 하므로 hello 액세스 토큰 만료 됩니다.
>  

또는에서 PowerShell toolog에서 REST 작업을 호출할 수 있습니다. Hello 인증 응답에서 다른 작업과 함께 사용 하기 위해 hello 액세스 토큰을 검색할 수 있습니다. REST 작업을 호출 하 여 hello 액세스 토큰을 검색 하는 예제를 보려면 [액세스 토큰 생성](resource-manager-rest-api.md#generating-an-access-token)합니다.

## <a name="debug"></a>디버그

서비스 사용자를 만들 때 다음 오류 hello를 발생할 수 있습니다.

* **"Authentication_Unauthorized"** 또는 **"hello 컨텍스트에서 구독이 찾을 수 있습니다."** -이 오류가 나타나는 hello 사용자 계정에 없을 때 [필요한 권한](#required-permissions) hello Azure Active Directory tooregister 응용 프로그램에 있습니다. 일반적으로 Azure Active Directory의 관리 사용자만 앱을 등록할 수 있고 사용자 계정은 관리자가 아니면 이 오류가 표시됩니다. 관리자 tooeither tooenable 사용자 tooregister 응용 프로그램이 나 있습니다 tooan 관리자 역할 할당을 요청 합니다.

* 계정 **"동작이 되어 있지 않습니다 권한 부여 tooperform 'Microsoft.Authorization/roleAssignments/write' 범위 ' / 구독 / {guid}'에 대해."**  -계정에 없을 때 충분 한 사용 권한을 tooassign 역할 tooan id를이 오류를 참조 하십시오. 구독 관리자 tooadd 요청 tooUser 액세스 관리자에 게 역할입니다.

## <a name="sample-applications"></a>샘플 응용 프로그램
서로 다른 플랫폼을 통해 응용 프로그램 hello로 로그인 하는 방법에 대 한 정보를 보려면

* [.NET](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [Java](/java/azure/java-sdk-azure-authenticate)
* [Node.JS](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [Python](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [Ruby](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a>다음 단계
* 리소스 관리를 위해 Azure에 응용 프로그램을 통합 하는 기능에 대 한 자세한 내용은 참조 하십시오. [hello Azure 리소스 관리자 API가 있는 개발자 가이드 tooauthorization](resource-manager-api-authentication.md)합니다.
* 응용 프로그램 및 서비스 주체에 대한 자세한 내용은 [응용 프로그램 개체 및 서비스 주체 개체](../active-directory/active-directory-application-objects.md)를 참조하세요. 
* Azure Active Directory 인증에 대한 자세한 내용은 [Azure AD의 인증 시나리오](../active-directory/active-directory-authentication-scenarios.md)를 참조하세요.
* 목록이 부여 하거나 거부 toousers 수 있는 작업에 대 한 참조 [Azure 리소스 관리자 리소스 공급자 작업](../active-directory/role-based-access-control-resource-provider-operations.md)합니다.

