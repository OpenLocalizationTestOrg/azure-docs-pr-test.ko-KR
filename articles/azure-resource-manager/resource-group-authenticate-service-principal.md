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
# <a name="use-azure-powershell-toocreate-a-service-principal-tooaccess-resources"></a><span data-ttu-id="2f5ce-104">Azure PowerShell toocreate 서비스 보안 주체 tooaccess 리소스 사용</span><span class="sxs-lookup"><span data-stu-id="2f5ce-104">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>

<span data-ttu-id="2f5ce-105">응용 프로그램 또는 스크립트를 tooaccess 리소스가 필요한 경우 hello 앱에 대 한 id를 설정할 수 있으며 자체 자격 증명으로 hello 앱을 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-105">When you have an app or script that needs tooaccess resources, you can set up an identity for hello app and authenticate hello app with its own credentials.</span></span> <span data-ttu-id="2f5ce-106">이 ID를 서비스 주체라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-106">This identity is known as a service principal.</span></span> <span data-ttu-id="2f5ce-107">이 접근 방법을 사용하면 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-107">This approach enables you to:</span></span>

* <span data-ttu-id="2f5ce-108">권한을 자신만 사용 권한을 것과 다른 toohello 응용 프로그램 id를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-108">Assign permissions toohello app identity that are different than your own permissions.</span></span> <span data-ttu-id="2f5ce-109">일반적으로 이러한 권한은 제한 된 tooexactly 어떤 hello 앱 toodo 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-109">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span>
* <span data-ttu-id="2f5ce-110">무인 스크립트를 실행할 때 인증을 위해 인증서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-110">Use a certificate for authentication when executing an unattended script.</span></span>

<span data-ttu-id="2f5ce-111">이 항목에서는 toouse [Azure PowerShell](/powershell/azure/overview) tooset 자체 자격 증명 및 id에서 응용 프로그램 toorun 프로그램에 필요한 모든 항목을 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-111">This topic shows you how toouse [Azure PowerShell](/powershell/azure/overview) tooset up everything you need for an application toorun under its own credentials and identity.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="2f5ce-112">필요한 사용 권한</span><span class="sxs-lookup"><span data-stu-id="2f5ce-112">Required permissions</span></span>
<span data-ttu-id="2f5ce-113">toocomplete이이 항목에서는 Azure Active Directory와 Azure 구독에서 충분 한 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-113">toocomplete this topic, you must have sufficient permissions in both your Azure Active Directory and your Azure subscription.</span></span> <span data-ttu-id="2f5ce-114">특히 수 toocreate hello Azure Active Directory에에서는 앱이 될 하 고 hello 서비스 보안 주체 tooa 역할을 할당 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-114">Specifically, you must be able toocreate an app in hello Azure Active Directory, and assign hello service principal tooa role.</span></span> 

<span data-ttu-id="2f5ce-115">hello 가장 쉬운 방법은 toocheck hello 포털을 통해이 계정을 적절 한 사용 권한이 있는지 여부.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-115">hello easiest way toocheck whether your account has adequate permissions is through hello portal.</span></span> <span data-ttu-id="2f5ce-116">[필요한 사용 권한 확인](resource-group-create-service-principal-portal.md#required-permissions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-116">See [Check required permission](resource-group-create-service-principal-portal.md#required-permissions).</span></span>

<span data-ttu-id="2f5ce-117">이제 tooa 섹션에 인증 하기 위해 계속 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-117">Now, proceed tooa section for authenticating with:</span></span>

* [<span data-ttu-id="2f5ce-118">암호</span><span class="sxs-lookup"><span data-stu-id="2f5ce-118">password</span></span>](#create-service-principal-with-password)
* [<span data-ttu-id="2f5ce-119">자체 서명된 인증서</span><span class="sxs-lookup"><span data-stu-id="2f5ce-119">self-signed certificate</span></span>](#create-service-principal-with-self-signed-certificate)
* [<span data-ttu-id="2f5ce-120">인증 기관의 인증서</span><span class="sxs-lookup"><span data-stu-id="2f5ce-120">certificate from Certificate Authority</span></span>](#create-service-principal-with-certificate-from-certificate-authority)

## <a name="powershell-commands"></a><span data-ttu-id="2f5ce-121">PowerShell 명령</span><span class="sxs-lookup"><span data-stu-id="2f5ce-121">PowerShell commands</span></span>

<span data-ttu-id="2f5ce-122">사용 서비스 사용자를 tooset, 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-122">tooset up a service principal, you use:</span></span>

| <span data-ttu-id="2f5ce-123">명령</span><span class="sxs-lookup"><span data-stu-id="2f5ce-123">Command</span></span> | <span data-ttu-id="2f5ce-124">설명</span><span class="sxs-lookup"><span data-stu-id="2f5ce-124">Description</span></span> |
| ------- | ----------- | 
| [<span data-ttu-id="2f5ce-125">New-AzureRmADServicePrincipal</span><span class="sxs-lookup"><span data-stu-id="2f5ce-125">New-AzureRmADServicePrincipal</span></span>](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | <span data-ttu-id="2f5ce-126">Azure Active Directory 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="2f5ce-126">Creates an Azure Active Directory service principal</span></span> |
| [<span data-ttu-id="2f5ce-127">New-AzureRmRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="2f5ce-127">New-AzureRmRoleAssignment</span></span>](/powershell/module/azurerm.resources/new-azurermroleassignment) | <span data-ttu-id="2f5ce-128">할당 hello RBAC 역할 toohello 지정한 보안 주체가 지정 된, hello에 범위를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-128">Assigns hello specified RBAC role toohello specified principal, at hello specified scope.</span></span> |


## <a name="create-service-principal-with-password"></a><span data-ttu-id="2f5ce-129">암호를 사용하여 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="2f5ce-129">Create service principal with password</span></span>

<span data-ttu-id="2f5ce-130">toocreate 구독에 대 한 hello 참가자 역할 인 서비스 사용자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-130">toocreate a service principal with hello Contributor role for your subscription, use:</span></span> 

```powershell
Login-AzureRmAccount
$sp = New-AzureRmADServicePrincipal -DisplayName exampleapp -Password "{provide-password}"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="2f5ce-131">hello 예제는 전체 Azure Active Directory에서 hello 제공 하는 서비스 새 주 toopropagate 약간의 시간이 tooallow 20 초 동안 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-131">hello example sleeps for 20 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="2f5ce-132">스크립트는 충분 한 시간 동안 대기 하지 않고 표시 한다는 오류: "PrincipalNotFound: 보안 주체 {id} hello 디렉터리에 존재 하지 않습니다."</span><span class="sxs-lookup"><span data-stu-id="2f5ce-132">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>

<span data-ttu-id="2f5ce-133">hello 다음 스크립트 toospecify hello 기본 구독 이외의 범위 있으며 오류가 발생할 경우 재시도 hello 역할 할당:</span><span class="sxs-lookup"><span data-stu-id="2f5ce-133">hello following script enables you toospecify a scope other than hello default subscription, and retries hello role assignment if an error occurs:</span></span>

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

<span data-ttu-id="2f5ce-134">Hello 스크립트에 대 한 몇 가지 항목 toonote:</span><span class="sxs-lookup"><span data-stu-id="2f5ce-134">A few items toonote about hello script:</span></span>

* <span data-ttu-id="2f5ce-135">toogrant hello identity 액세스 toohello 기본 구독 않아도 tooprovide ResourceGroup 또는 SubscriptionId 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-135">toogrant hello identity access toohello default subscription, you do not need tooprovide either ResourceGroup or SubscriptionId parameters.</span></span>
* <span data-ttu-id="2f5ce-136">Toolimit hello 범위 hello 역할 할당 tooa 리소스 그룹의 경우에 hello ResourceGroup 매개 변수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-136">Specify hello ResourceGroup parameter only when you want toolimit hello scope of hello role assignment tooa resource group.</span></span>
*  <span data-ttu-id="2f5ce-137">이 예제에서는 hello 서비스 보안 주체 toohello 참가자 역할을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-137">In this example, you add hello service principal toohello Contributor role.</span></span> <span data-ttu-id="2f5ce-138">다른 역할에 대해서는 [RBAC: 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-138">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="2f5ce-139">hello 스크립트는 전체 Azure Active Directory에서 hello 제공 하는 서비스 새 주 toopropagate 약간의 시간이 tooallow 15 초 동안 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-139">hello script sleeps for 15 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="2f5ce-140">스크립트는 충분 한 시간 동안 대기 하지 않고 표시 한다는 오류: "PrincipalNotFound: 보안 주체 {id} hello 디렉터리에 존재 하지 않습니다."</span><span class="sxs-lookup"><span data-stu-id="2f5ce-140">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>
* <span data-ttu-id="2f5ce-141">Toogrant hello 서비스 보안 주체 액세스 toomore 구독 또는 리소스 그룹을 해야 하는 경우 실행 hello `New-AzureRMRoleAssignment` 다양 한 범위를 사용 하 여 다시 cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-141">If you need toogrant hello service principal access toomore subscriptions or resource groups, run hello `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>


### <a name="provide-credentials-through-powershell"></a><span data-ttu-id="2f5ce-142">PowerShell을 통해 자격 증명 제공</span><span class="sxs-lookup"><span data-stu-id="2f5ce-142">Provide credentials through PowerShell</span></span>
<span data-ttu-id="2f5ce-143">이제, hello 응용 프로그램 tooperform 작업으로 toolog에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-143">Now, you need toolog in as hello application tooperform operations.</span></span> <span data-ttu-id="2f5ce-144">Hello 사용자 이름에 대 한 hello를 사용 하 여 `ApplicationId` hello 응용 프로그램에 대해 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-144">For hello user name, use hello `ApplicationId` that you created for hello application.</span></span> <span data-ttu-id="2f5ce-145">Hello 암호에 대 한 hello hello 계정을 만들 때 지정 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-145">For hello password, use hello one you specified when creating hello account.</span></span> 

```powershell   
$creds = Get-Credential
Login-AzureRmAccount -Credential $creds -ServicePrincipal -TenantId {tenant-id}
```

<span data-ttu-id="2f5ce-146">테 넌 트 ID hello/소문자를 구분 하지 않으므로 스크립트에서 직접 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-146">hello tenant ID is not sensitive, so you can embed it directly in your script.</span></span> <span data-ttu-id="2f5ce-147">Tooretrieve hello 테 넌 트 ID, 필요한 경우 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-147">If you need tooretrieve hello tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

## <a name="create-service-principal-with-self-signed-certificate"></a><span data-ttu-id="2f5ce-148">자체 서명된 인증서를 사용하여 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="2f5ce-148">Create service principal with self-signed certificate</span></span>

<span data-ttu-id="2f5ce-149">toocreate 자체 서명 된 인증서와 구독에 대 한 hello 참가자 역할 서비스 사용자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-149">toocreate a service principal with a self-signed certificate and hello Contributor role for your subscription, use:</span></span> 

```powershell
Login-AzureRmAccount
$cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=exampleappScriptCert" -KeySpec KeyExchange
$keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())

$sp = New-AzureRMADServicePrincipal -DisplayName exampleapp -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="2f5ce-150">hello 예제는 전체 Azure Active Directory에서 hello 제공 하는 서비스 새 주 toopropagate 약간의 시간이 tooallow 20 초 동안 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-150">hello example sleeps for 20 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="2f5ce-151">스크립트는 충분 한 시간 동안 대기 하지 않고 표시 한다는 오류: "PrincipalNotFound: 보안 주체 {id} hello 디렉터리에 존재 하지 않습니다."</span><span class="sxs-lookup"><span data-stu-id="2f5ce-151">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>

<span data-ttu-id="2f5ce-152">hello 다음 스크립트 toospecify hello 기본 구독 이외의 범위 있으며 오류가 발생할 경우 재시도 hello 역할 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-152">hello following script enables you toospecify a scope other than hello default subscription, and retries hello role assignment if an error occurs.</span></span> <span data-ttu-id="2f5ce-153">Windows 10 또는 Windows Server 2016에서 Azure PowerShell 2.0이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-153">You must have Azure PowerShell 2.0 on Windows 10 or Windows Server 2016.</span></span>

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

<span data-ttu-id="2f5ce-154">Hello 스크립트에 대 한 몇 가지 항목 toonote:</span><span class="sxs-lookup"><span data-stu-id="2f5ce-154">A few items toonote about hello script:</span></span>

* <span data-ttu-id="2f5ce-155">toogrant hello identity 액세스 toohello 기본 구독 않아도 tooprovide ResourceGroup 또는 SubscriptionId 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-155">toogrant hello identity access toohello default subscription, you do not need tooprovide either ResourceGroup or SubscriptionId parameters.</span></span>
* <span data-ttu-id="2f5ce-156">Toolimit hello 범위 hello 역할 할당 tooa 리소스 그룹의 경우에 hello ResourceGroup 매개 변수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-156">Specify hello ResourceGroup parameter only when you want toolimit hello scope of hello role assignment tooa resource group.</span></span>
* <span data-ttu-id="2f5ce-157">이 예제에서는 hello 서비스 보안 주체 toohello 참가자 역할을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-157">In this example, you add hello service principal toohello Contributor role.</span></span> <span data-ttu-id="2f5ce-158">다른 역할에 대해서는 [RBAC: 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-158">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="2f5ce-159">hello 스크립트는 전체 Azure Active Directory에서 hello 제공 하는 서비스 새 주 toopropagate 약간의 시간이 tooallow 15 초 동안 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-159">hello script sleeps for 15 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="2f5ce-160">스크립트는 충분 한 시간 동안 대기 하지 않고 표시 한다는 오류: "PrincipalNotFound: 보안 주체 {id} hello 디렉터리에 존재 하지 않습니다."</span><span class="sxs-lookup"><span data-stu-id="2f5ce-160">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>
* <span data-ttu-id="2f5ce-161">Toogrant hello 서비스 보안 주체 액세스 toomore 구독 또는 리소스 그룹을 해야 하는 경우 실행 hello `New-AzureRMRoleAssignment` 다양 한 범위를 사용 하 여 다시 cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-161">If you need toogrant hello service principal access toomore subscriptions or resource groups, run hello `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>

<span data-ttu-id="2f5ce-162">경우 있습니다 **Windows 10 또는 Windows Server 2016 Technical Preview 없는**, toodownload hello 해야 [자체 서명 된 인증서 생성기](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) Microsoft 스크립트 센터에서.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-162">If you **do not have Windows 10 or Windows Server 2016 Technical Preview**, you need toodownload hello [Self-signed certificate generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) from Microsoft Script Center.</span></span> <span data-ttu-id="2f5ce-163">콘텐츠를 추출 하 고 필요한 hello cmdlet을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-163">Extract its contents and import hello cmdlet you need.</span></span>

```powershell  
# Only run if you could not use New-SelfSignedCertificate
Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
```
  
<span data-ttu-id="2f5ce-164">Hello 스크립트에서 다음 두 줄 toogenerate hello 인증서 hello를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-164">In hello script, substitute hello following two lines toogenerate hello certificate.</span></span>
  
```powershell
New-SelfSignedCertificateEx  -StoreLocation CurrentUser -StoreName My -Subject "CN=exampleapp" -KeySpec "Exchange" -FriendlyName "exampleapp"
$cert = Get-ChildItem -path Cert:\CurrentUser\my | where {$PSitem.Subject -eq 'CN=exampleapp' }
```

### <a name="provide-certificate-through-automated-powershell-script"></a><span data-ttu-id="2f5ce-165">자동화된 PowerShell 스크립트를 통해 인증서 제공</span><span class="sxs-lookup"><span data-stu-id="2f5ce-165">Provide certificate through automated PowerShell script</span></span>
<span data-ttu-id="2f5ce-166">서비스 사용자로 로그인 할 때마다 AD 앱에 대 한 hello 디렉터리의 tooprovide hello 테 넌 트 id가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-166">Whenever you sign in as a service principal, you need tooprovide hello tenant id of hello directory for your AD app.</span></span> <span data-ttu-id="2f5ce-167">테넌트는 Azure Active Directory의 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-167">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="2f5ce-168">구독이 하나만 있는 경우 다음을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-168">If you only have one subscription, you can use:</span></span>

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

<span data-ttu-id="2f5ce-169">ID 및 테 넌 트 ID hello 응용 프로그램/소문자를 구분 하지 않으므로 스크립트에서 직접 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-169">hello application ID and tenant ID are not sensitive, so you can embed them directly in your script.</span></span> <span data-ttu-id="2f5ce-170">Tooretrieve hello 테 넌 트 ID, 필요한 경우 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-170">If you need tooretrieve hello tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

<span data-ttu-id="2f5ce-171">Tooretrieve hello 응용 프로그램 ID, 필요한 경우 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-171">If you need tooretrieve hello application ID, use:</span></span>

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="create-service-principal-with-certificate-from-certificate-authority"></a><span data-ttu-id="2f5ce-172">인증 기관의 인증서를 사용하여 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="2f5ce-172">Create service principal with certificate from Certificate Authority</span></span>
<span data-ttu-id="2f5ce-173">인증 기관 toocreate 서비스 사용자를 사용 하 여 hello 다음 스크립트에서 발급 한 인증서 toouse:</span><span class="sxs-lookup"><span data-stu-id="2f5ce-173">toouse a certificate issued from a Certificate Authority toocreate service principal, use hello following script:</span></span>

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

<span data-ttu-id="2f5ce-174">Hello 스크립트에 대 한 몇 가지 항목 toonote:</span><span class="sxs-lookup"><span data-stu-id="2f5ce-174">A few items toonote about hello script:</span></span>

* <span data-ttu-id="2f5ce-175">액세스 범위 지정 된 toohello 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-175">Access is scoped toohello subscription.</span></span>
* <span data-ttu-id="2f5ce-176">이 예제에서는 hello 서비스 보안 주체 toohello 참가자 역할을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-176">In this example, you add hello service principal toohello Contributor role.</span></span> <span data-ttu-id="2f5ce-177">다른 역할에 대해서는 [RBAC: 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-177">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="2f5ce-178">hello 스크립트는 전체 Azure Active Directory에서 hello 제공 하는 서비스 새 주 toopropagate 약간의 시간이 tooallow 15 초 동안 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-178">hello script sleeps for 15 seconds tooallow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="2f5ce-179">스크립트는 충분 한 시간 동안 대기 하지 않고 표시 한다는 오류: "PrincipalNotFound: 보안 주체 {id} hello 디렉터리에 존재 하지 않습니다."</span><span class="sxs-lookup"><span data-stu-id="2f5ce-179">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in hello directory."</span></span>
* <span data-ttu-id="2f5ce-180">Toogrant hello 서비스 보안 주체 액세스 toomore 구독 또는 리소스 그룹을 해야 하는 경우 실행 hello `New-AzureRMRoleAssignment` 다양 한 범위를 사용 하 여 다시 cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-180">If you need toogrant hello service principal access toomore subscriptions or resource groups, run hello `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>

### <a name="provide-certificate-through-automated-powershell-script"></a><span data-ttu-id="2f5ce-181">자동화된 PowerShell 스크립트를 통해 인증서 제공</span><span class="sxs-lookup"><span data-stu-id="2f5ce-181">Provide certificate through automated PowerShell script</span></span>
<span data-ttu-id="2f5ce-182">서비스 사용자로 로그인 할 때마다 AD 앱에 대 한 hello 디렉터리의 tooprovide hello 테 넌 트 id가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-182">Whenever you sign in as a service principal, you need tooprovide hello tenant id of hello directory for your AD app.</span></span> <span data-ttu-id="2f5ce-183">테넌트는 Azure Active Directory의 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-183">A tenant is an instance of Azure Active Directory.</span></span>

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

<span data-ttu-id="2f5ce-184">ID 및 테 넌 트 ID hello 응용 프로그램/소문자를 구분 하지 않으므로 스크립트에서 직접 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-184">hello application ID and tenant ID are not sensitive, so you can embed them directly in your script.</span></span> <span data-ttu-id="2f5ce-185">Tooretrieve hello 테 넌 트 ID, 필요한 경우 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-185">If you need tooretrieve hello tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

<span data-ttu-id="2f5ce-186">Tooretrieve hello 응용 프로그램 ID, 필요한 경우 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-186">If you need tooretrieve hello application ID, use:</span></span>

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="change-credentials"></a><span data-ttu-id="2f5ce-187">자격 증명 변경</span><span class="sxs-lookup"><span data-stu-id="2f5ce-187">Change credentials</span></span>

<span data-ttu-id="2f5ce-188">hello를 사용 하는 보안 또는 자격 증명 만료 때문에 AD 응용 프로그램에 대 한 toochange hello 자격 [제거 AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) 및 [새로 AzureRmADAppCredential](/powershell/module/azurerm.resources/new-azurermadappcredential) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-188">toochange hello credentials for an AD app, either because of a security compromise or a credential expiration, use hello [Remove-AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) and [New-AzureRmADAppCredential](/powershell/module/azurerm.resources/new-azurermadappcredential) cmdlets.</span></span>

<span data-ttu-id="2f5ce-189">tooremove 응용 프로그램에 대 한 모든 hello 자격 증명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-189">tooremove all hello credentials for an application, use:</span></span>

```powershell
Remove-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -All
```

<span data-ttu-id="2f5ce-190">tooadd 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-190">tooadd a password, use:</span></span>

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -Password p@ssword!
```

<span data-ttu-id="2f5ce-191">이 항목에 표시 된 대로 tooadd 인증서 값 자체 서명 된 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-191">tooadd a certificate value, create a self-signed certificate as shown in this topic.</span></span> <span data-ttu-id="2f5ce-192">그 후 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-192">Then, use:</span></span>

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
```

## <a name="save-access-token-toosimplify-log-in"></a><span data-ttu-id="2f5ce-193">액세스 토큰 toosimplify 로그인 저장</span><span class="sxs-lookup"><span data-stu-id="2f5ce-193">Save access token toosimplify log in</span></span>
<span data-ttu-id="2f5ce-194">tooavoid 제공 hello 서비스 사용자 자격 증명에 toolog 해야 할 때마다 hello 액세스 토큰을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-194">tooavoid providing hello service principal credentials every time it needs toolog in, you can save hello access token.</span></span>

<span data-ttu-id="2f5ce-195">이후 세션에서 toouse hello 현재 액세스 토큰이 hello 프로필을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-195">toouse hello current access token in a later session, save hello profile.</span></span>
   
```powershell
Save-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```
   
<span data-ttu-id="2f5ce-196">Hello 프로필 열고 해당 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-196">Open hello profile and examine its contents.</span></span> <span data-ttu-id="2f5ce-197">액세스 토큰을 포함하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-197">Notice that it contains an access token.</span></span> <span data-ttu-id="2f5ce-198">수동으로 다시 로그인을 대신 단순히 hello 프로필을 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-198">Instead of manually logging in again, simply load hello profile.</span></span>
   
```powershell
Select-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```

> [!NOTE]
> <span data-ttu-id="2f5ce-199">저장된 된 프로필을 사용 하 여만 작동에 대 한 hello 토큰은 유효 하므로 hello 액세스 토큰 만료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-199">hello access token expires, so using a saved profile only works for as long as hello token is valid.</span></span>
>  

<span data-ttu-id="2f5ce-200">또는에서 PowerShell toolog에서 REST 작업을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-200">Alternatively, you can invoke REST operations from PowerShell toolog in.</span></span> <span data-ttu-id="2f5ce-201">Hello 인증 응답에서 다른 작업과 함께 사용 하기 위해 hello 액세스 토큰을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-201">From hello authentication response, you can retrieve hello access token for use with other operations.</span></span> <span data-ttu-id="2f5ce-202">REST 작업을 호출 하 여 hello 액세스 토큰을 검색 하는 예제를 보려면 [액세스 토큰 생성](resource-manager-rest-api.md#generating-an-access-token)합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-202">For an example of retrieving hello access token by invoking REST operations, see [Generating an Access Token](resource-manager-rest-api.md#generating-an-access-token).</span></span>

## <a name="debug"></a><span data-ttu-id="2f5ce-203">디버그</span><span class="sxs-lookup"><span data-stu-id="2f5ce-203">Debug</span></span>

<span data-ttu-id="2f5ce-204">서비스 사용자를 만들 때 다음 오류 hello를 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-204">You may encounter hello following errors when creating a service principal:</span></span>

* <span data-ttu-id="2f5ce-205">**"Authentication_Unauthorized"** 또는 **"hello 컨텍스트에서 구독이 찾을 수 있습니다."**</span><span class="sxs-lookup"><span data-stu-id="2f5ce-205">**"Authentication_Unauthorized"** or **"No subscription found in hello context."**</span></span> <span data-ttu-id="2f5ce-206">-이 오류가 나타나는 hello 사용자 계정에 없을 때 [필요한 권한](#required-permissions) hello Azure Active Directory tooregister 응용 프로그램에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-206">- You see this error when your account does not have hello [required permissions](#required-permissions) on hello Azure Active Directory tooregister an app.</span></span> <span data-ttu-id="2f5ce-207">일반적으로 Azure Active Directory의 관리 사용자만 앱을 등록할 수 있고 사용자 계정은 관리자가 아니면 이 오류가 표시됩니다. 관리자 tooeither tooenable 사용자 tooregister 응용 프로그램이 나 있습니다 tooan 관리자 역할 할당을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-207">Typically, you see this error when only admin users in your Azure Active Directory can register apps, and your account is not an admin. Ask your administrator tooeither assign you tooan administrator role, or tooenable users tooregister apps.</span></span>

* <span data-ttu-id="2f5ce-208">계정 **"동작이 되어 있지 않습니다 권한 부여 tooperform 'Microsoft.Authorization/roleAssignments/write' 범위 ' / 구독 / {guid}'에 대해."**  -계정에 없을 때 충분 한 사용 권한을 tooassign 역할 tooan id를이 오류를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-208">Your account **"does not have authorization tooperform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/{guid}'."** - You see this error when your account does not have sufficient permissions tooassign a role tooan identity.</span></span> <span data-ttu-id="2f5ce-209">구독 관리자 tooadd 요청 tooUser 액세스 관리자에 게 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-209">Ask your subscription administrator tooadd you tooUser Access Administrator role.</span></span>

## <a name="sample-applications"></a><span data-ttu-id="2f5ce-210">샘플 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="2f5ce-210">Sample applications</span></span>
<span data-ttu-id="2f5ce-211">서로 다른 플랫폼을 통해 응용 프로그램 hello로 로그인 하는 방법에 대 한 정보를 보려면</span><span class="sxs-lookup"><span data-stu-id="2f5ce-211">For information about logging in as hello application through different platforms, see:</span></span>

* [<span data-ttu-id="2f5ce-212">.NET</span><span class="sxs-lookup"><span data-stu-id="2f5ce-212">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="2f5ce-213">Java</span><span class="sxs-lookup"><span data-stu-id="2f5ce-213">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="2f5ce-214">Node.JS</span><span class="sxs-lookup"><span data-stu-id="2f5ce-214">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="2f5ce-215">Python</span><span class="sxs-lookup"><span data-stu-id="2f5ce-215">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="2f5ce-216">Ruby</span><span class="sxs-lookup"><span data-stu-id="2f5ce-216">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a><span data-ttu-id="2f5ce-217">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2f5ce-217">Next steps</span></span>
* <span data-ttu-id="2f5ce-218">리소스 관리를 위해 Azure에 응용 프로그램을 통합 하는 기능에 대 한 자세한 내용은 참조 하십시오. [hello Azure 리소스 관리자 API가 있는 개발자 가이드 tooauthorization](resource-manager-api-authentication.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-218">For detailed steps on integrating an application into Azure for managing resources, see [Developer's guide tooauthorization with hello Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="2f5ce-219">응용 프로그램 및 서비스 주체에 대한 자세한 내용은 [응용 프로그램 개체 및 서비스 주체 개체](../active-directory/active-directory-application-objects.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-219">For a more detailed explanation of applications and service principals, see [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span> 
* <span data-ttu-id="2f5ce-220">Azure Active Directory 인증에 대한 자세한 내용은 [Azure AD의 인증 시나리오](../active-directory/active-directory-authentication-scenarios.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-220">For more information about Azure Active Directory authentication, see [Authentication Scenarios for Azure AD](../active-directory/active-directory-authentication-scenarios.md).</span></span>
* <span data-ttu-id="2f5ce-221">목록이 부여 하거나 거부 toousers 수 있는 작업에 대 한 참조 [Azure 리소스 관리자 리소스 공급자 작업](../active-directory/role-based-access-control-resource-provider-operations.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2f5ce-221">For a list of available actions that can be granted or denied toousers, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>

