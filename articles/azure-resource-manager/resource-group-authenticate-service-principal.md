---
title: "PowerShell을 사용하여 Azure 앱에 대한 ID 만들기 | Microsoft Docs"
description: "Azure PowerShell을 사용하여 Azure Active Directory 응용 프로그램 및 서비스 주체를 만들고 역할 기반 액세스 제어를 통해 리소스에 대한 액세스를 부여하는 방법을 설명합니다. 암호 또는 인증서를 사용하여 응용 프로그램을 인증하는 방법을 보여 줍니다."
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
ms.openlocfilehash: 55e83b0742652abbb42100a11a468bc13a7a8aed
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="use-azure-powershell-to-create-a-service-principal-to-access-resources"></a><span data-ttu-id="ebba9-104">Azure PowerShell을 사용하여 리소스에 액세스하는 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="ebba9-104">Use Azure PowerShell to create a service principal to access resources</span></span>

<span data-ttu-id="ebba9-105">리소스에 액세스해야 하는 앱 또는 스크립트가 있는 경우 앱에 대한 ID를 설정하고 자체 자격 증명으로 앱을 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-105">When you have an app or script that needs to access resources, you can set up an identity for the app and authenticate the app with its own credentials.</span></span> <span data-ttu-id="ebba9-106">이 ID를 서비스 주체라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-106">This identity is known as a service principal.</span></span> <span data-ttu-id="ebba9-107">이 접근 방법을 사용하면 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-107">This approach enables you to:</span></span>

* <span data-ttu-id="ebba9-108">자체 사용 권한과 다른 앱 ID에 대한 사용 권한을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-108">Assign permissions to the app identity that are different than your own permissions.</span></span> <span data-ttu-id="ebba9-109">일반적으로 이러한 권한은 정확히 앱 실행에 필요한 것으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-109">Typically, these permissions are restricted to exactly what the app needs to do.</span></span>
* <span data-ttu-id="ebba9-110">무인 스크립트를 실행할 때 인증을 위해 인증서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-110">Use a certificate for authentication when executing an unattended script.</span></span>

<span data-ttu-id="ebba9-111">이 토픽에서는 [Azure PowerShell](/powershell/azure/overview) 을 사용하여 응용 프로그램을 자체 자격 증명 및 ID로 실행하는 데 필요한 모든 항목을 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-111">This topic shows you how to use [Azure PowerShell](/powershell/azure/overview) to set up everything you need for an application to run under its own credentials and identity.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="ebba9-112">필요한 사용 권한</span><span class="sxs-lookup"><span data-stu-id="ebba9-112">Required permissions</span></span>
<span data-ttu-id="ebba9-113">이 항목을 완료하려면 Azure Active Directory와 Azure 구독에 대한 충분한 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-113">To complete this topic, you must have sufficient permissions in both your Azure Active Directory and your Azure subscription.</span></span> <span data-ttu-id="ebba9-114">특히, Azure Active Directory에서 앱을 만들고 역할에 서비스 주체를 할당할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-114">Specifically, you must be able to create an app in the Azure Active Directory, and assign the service principal to a role.</span></span> 

<span data-ttu-id="ebba9-115">계정에 적절한 사용 권한이 있는지를 확인하는 가장 쉬운 방법은 포털을 통하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-115">The easiest way to check whether your account has adequate permissions is through the portal.</span></span> <span data-ttu-id="ebba9-116">[필요한 사용 권한 확인](resource-group-create-service-principal-portal.md#required-permissions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebba9-116">See [Check required permission](resource-group-create-service-principal-portal.md#required-permissions).</span></span>

<span data-ttu-id="ebba9-117">이제 다음을 사용하여 인증을 받기 위한 섹션을 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-117">Now, proceed to a section for authenticating with:</span></span>

* [<span data-ttu-id="ebba9-118">암호</span><span class="sxs-lookup"><span data-stu-id="ebba9-118">password</span></span>](#create-service-principal-with-password)
* [<span data-ttu-id="ebba9-119">자체 서명된 인증서</span><span class="sxs-lookup"><span data-stu-id="ebba9-119">self-signed certificate</span></span>](#create-service-principal-with-self-signed-certificate)
* [<span data-ttu-id="ebba9-120">인증 기관의 인증서</span><span class="sxs-lookup"><span data-stu-id="ebba9-120">certificate from Certificate Authority</span></span>](#create-service-principal-with-certificate-from-certificate-authority)

## <a name="powershell-commands"></a><span data-ttu-id="ebba9-121">PowerShell 명령</span><span class="sxs-lookup"><span data-stu-id="ebba9-121">PowerShell commands</span></span>

<span data-ttu-id="ebba9-122">서비스 주체를 설정하려면 다음 항목을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-122">To set up a service principal, you use:</span></span>

| <span data-ttu-id="ebba9-123">명령</span><span class="sxs-lookup"><span data-stu-id="ebba9-123">Command</span></span> | <span data-ttu-id="ebba9-124">설명</span><span class="sxs-lookup"><span data-stu-id="ebba9-124">Description</span></span> |
| ------- | ----------- | 
| [<span data-ttu-id="ebba9-125">New-AzureRmADServicePrincipal</span><span class="sxs-lookup"><span data-stu-id="ebba9-125">New-AzureRmADServicePrincipal</span></span>](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | <span data-ttu-id="ebba9-126">Azure Active Directory 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="ebba9-126">Creates an Azure Active Directory service principal</span></span> |
| [<span data-ttu-id="ebba9-127">New-AzureRmRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="ebba9-127">New-AzureRmRoleAssignment</span></span>](/powershell/module/azurerm.resources/new-azurermroleassignment) | <span data-ttu-id="ebba9-128">지정된 범위에서 지정된 보안 주체에 지정된 RBAC 역할을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-128">Assigns the specified RBAC role to the specified principal, at the specified scope.</span></span> |


## <a name="create-service-principal-with-password"></a><span data-ttu-id="ebba9-129">암호를 사용하여 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="ebba9-129">Create service principal with password</span></span>

<span data-ttu-id="ebba9-130">구독에 대해 참여자 역할을 가진 서비스 주체를 만들려면 다음 항목을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-130">To create a service principal with the Contributor role for your subscription, use:</span></span> 

```powershell
Login-AzureRmAccount
$sp = New-AzureRmADServicePrincipal -DisplayName exampleapp -Password "{provide-password}"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="ebba9-131">이 예제는 새 서비스 주체가 Azure Active Directory 전체에 전파될 시간을 허용하기 위해 20분간 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-131">The example sleeps for 20 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="ebba9-132">스크립트가 대기하는 시간이 충분히 길지 않으면 "PrincipalNotFound: 보안 주체 {id}이(가) 디렉터리에 없습니다."라는 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-132">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span></span>

<span data-ttu-id="ebba9-133">다음 스크립트를 통해 기본 구독 이외의 범위를 지정하고 오류가 발생하는 경우 역할 할당을 다시 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-133">The following script enables you to specify a scope other than the default subscription, and retries the role assignment if an error occurs:</span></span>

```powershell
Param (

 # Use to set scope to resource group. If no value is provided, scope is set to subscription.
 [Parameter(Mandatory=$false)]
 [String] $ResourceGroup,

 # Use to set subscription. If no value is provided, default subscription is used. 
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

 
 # Create Service Principal for the AD app
 $ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -Password $Password
 Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 

 $NewRole = $null
 $Retries = 0;
 While ($NewRole -eq $null -and $Retries -le 6)
 {
    # Sleep here for a few seconds to allow the service principal application to become active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
```

<span data-ttu-id="ebba9-134">스크립트에 대해 다음 사항을 알아두세요.</span><span class="sxs-lookup"><span data-stu-id="ebba9-134">A few items to note about the script:</span></span>

* <span data-ttu-id="ebba9-135">ID에기본 구독에 대한 액세스 권한을 부여하기 위해 ResourceGroup 또는 SubscriptionId 매개 변수를 제공할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-135">To grant the identity access to the default subscription, you do not need to provide either ResourceGroup or SubscriptionId parameters.</span></span>
* <span data-ttu-id="ebba9-136">역할 할당의 범위를 리소스 그룹으로 제한하려는 경우에만 ResourceGroup 매개 변수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-136">Specify the ResourceGroup parameter only when you want to limit the scope of the role assignment to a resource group.</span></span>
*  <span data-ttu-id="ebba9-137">이 예제에서는 참가자 역할에 서비스 주체를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-137">In this example, you add the service principal to the Contributor role.</span></span> <span data-ttu-id="ebba9-138">다른 역할에 대해서는 [RBAC: 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebba9-138">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="ebba9-139">이 스크립트는 새 서비스 주체가 Azure Active Directory 전체에 전파될 시간을 허용하기 위해 15분간 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-139">The script sleeps for 15 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="ebba9-140">스크립트가 대기하는 시간이 충분히 길지 않으면 "PrincipalNotFound: 보안 주체 {id}이(가) 디렉터리에 없습니다."라는 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-140">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span></span>
* <span data-ttu-id="ebba9-141">서비스 주체에게 더 많은 구독 또는 리소스 그룹에 대한 액세스 권한을 부여해야 할 경우 다른 범위를 지정해서 `New-AzureRMRoleAssignment` cmdlet을 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-141">If you need to grant the service principal access to more subscriptions or resource groups, run the `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>


### <a name="provide-credentials-through-powershell"></a><span data-ttu-id="ebba9-142">PowerShell을 통해 자격 증명 제공</span><span class="sxs-lookup"><span data-stu-id="ebba9-142">Provide credentials through PowerShell</span></span>
<span data-ttu-id="ebba9-143">이제 응용 프로그램으로 로그인하여 작업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-143">Now, you need to log in as the application to perform operations.</span></span> <span data-ttu-id="ebba9-144">사용자 이름으로 응용 프로그램에 대해 만든 `ApplicationId`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-144">For the user name, use the `ApplicationId` that you created for the application.</span></span> <span data-ttu-id="ebba9-145">암호의 경우 계정을 만들 때 지정한 암호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-145">For the password, use the one you specified when creating the account.</span></span> 

```powershell   
$creds = Get-Credential
Login-AzureRmAccount -Credential $creds -ServicePrincipal -TenantId {tenant-id}
```

<span data-ttu-id="ebba9-146">테넌트 ID는 대/소문자를 구분하지 않으므로 스크립트에 직접 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-146">The tenant ID is not sensitive, so you can embed it directly in your script.</span></span> <span data-ttu-id="ebba9-147">테넌트 ID를 검색해야 할 경우 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-147">If you need to retrieve the tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

## <a name="create-service-principal-with-self-signed-certificate"></a><span data-ttu-id="ebba9-148">자체 서명된 인증서를 사용하여 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="ebba9-148">Create service principal with self-signed certificate</span></span>

<span data-ttu-id="ebba9-149">구독에 대해 자체 서명된 인증서 및 참여자 역할을 가진 서비스 주체를 만들려면 다음 항목을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-149">To create a service principal with a self-signed certificate and the Contributor role for your subscription, use:</span></span> 

```powershell
Login-AzureRmAccount
$cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=exampleappScriptCert" -KeySpec KeyExchange
$keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())

$sp = New-AzureRMADServicePrincipal -DisplayName exampleapp -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="ebba9-150">이 예제는 새 서비스 주체가 Azure Active Directory 전체에 전파될 시간을 허용하기 위해 20분간 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-150">The example sleeps for 20 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="ebba9-151">스크립트가 대기하는 시간이 충분히 길지 않으면 "PrincipalNotFound: 보안 주체 {id}이(가) 디렉터리에 없습니다."라는 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-151">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span></span>

<span data-ttu-id="ebba9-152">다음 스크립트를 통해 기본 구독 이외의 범위를 지정하고 오류가 발생하는 경우 역할 할당을 다시 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-152">The following script enables you to specify a scope other than the default subscription, and retries the role assignment if an error occurs.</span></span> <span data-ttu-id="ebba9-153">Windows 10 또는 Windows Server 2016에서 Azure PowerShell 2.0이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-153">You must have Azure PowerShell 2.0 on Windows 10 or Windows Server 2016.</span></span>

```powershell
Param (

 # Use to set scope to resource group. If no value is provided, scope is set to subscription.
 [Parameter(Mandatory=$false)]
 [String] $ResourceGroup,

 # Use to set subscription. If no value is provided, default subscription is used. 
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
    # Sleep here for a few seconds to allow the service principal application to become active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
```

<span data-ttu-id="ebba9-154">스크립트에 대해 다음 사항을 알아두세요.</span><span class="sxs-lookup"><span data-stu-id="ebba9-154">A few items to note about the script:</span></span>

* <span data-ttu-id="ebba9-155">ID에기본 구독에 대한 액세스 권한을 부여하기 위해 ResourceGroup 또는 SubscriptionId 매개 변수를 제공할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-155">To grant the identity access to the default subscription, you do not need to provide either ResourceGroup or SubscriptionId parameters.</span></span>
* <span data-ttu-id="ebba9-156">역할 할당의 범위를 리소스 그룹으로 제한하려는 경우에만 ResourceGroup 매개 변수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-156">Specify the ResourceGroup parameter only when you want to limit the scope of the role assignment to a resource group.</span></span>
* <span data-ttu-id="ebba9-157">이 예제에서는 참가자 역할에 서비스 주체를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-157">In this example, you add the service principal to the Contributor role.</span></span> <span data-ttu-id="ebba9-158">다른 역할에 대해서는 [RBAC: 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebba9-158">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="ebba9-159">이 스크립트는 새 서비스 주체가 Azure Active Directory 전체에 전파될 시간을 허용하기 위해 15분간 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-159">The script sleeps for 15 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="ebba9-160">스크립트가 대기하는 시간이 충분히 길지 않으면 "PrincipalNotFound: 보안 주체 {id}이(가) 디렉터리에 없습니다."라는 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-160">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span></span>
* <span data-ttu-id="ebba9-161">서비스 주체에게 더 많은 구독 또는 리소스 그룹에 대한 액세스 권한을 부여해야 할 경우 다른 범위를 지정해서 `New-AzureRMRoleAssignment` cmdlet을 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-161">If you need to grant the service principal access to more subscriptions or resource groups, run the `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>

<span data-ttu-id="ebba9-162">**Windows 10 또는 Windows Server 2016 Technical Preview**사용자가 아니라면 Microsoft Script Center에서 [Self-signed certificate generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) 를 다운로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-162">If you **do not have Windows 10 or Windows Server 2016 Technical Preview**, you need to download the [Self-signed certificate generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) from Microsoft Script Center.</span></span> <span data-ttu-id="ebba9-163">해당 내용을 추출하고 필요한 cmdlet을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-163">Extract its contents and import the cmdlet you need.</span></span>

```powershell  
# Only run if you could not use New-SelfSignedCertificate
Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
```
  
<span data-ttu-id="ebba9-164">스크립트에서 다음 두 줄을 바꾸어 인증서를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-164">In the script, substitute the following two lines to generate the certificate.</span></span>
  
```powershell
New-SelfSignedCertificateEx  -StoreLocation CurrentUser -StoreName My -Subject "CN=exampleapp" -KeySpec "Exchange" -FriendlyName "exampleapp"
$cert = Get-ChildItem -path Cert:\CurrentUser\my | where {$PSitem.Subject -eq 'CN=exampleapp' }
```

### <a name="provide-certificate-through-automated-powershell-script"></a><span data-ttu-id="ebba9-165">자동화된 PowerShell 스크립트를 통해 인증서 제공</span><span class="sxs-lookup"><span data-stu-id="ebba9-165">Provide certificate through automated PowerShell script</span></span>
<span data-ttu-id="ebba9-166">서비스 주체로 로그인할 때마다 AD 앱에 디렉터리의 테넌트 ID를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-166">Whenever you sign in as a service principal, you need to provide the tenant id of the directory for your AD app.</span></span> <span data-ttu-id="ebba9-167">테넌트는 Azure Active Directory의 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-167">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="ebba9-168">구독이 하나만 있는 경우 다음을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-168">If you only have one subscription, you can use:</span></span>

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

<span data-ttu-id="ebba9-169">응용 프로그램 ID 및 테넌트 ID는 대/소문자를 구분하지 않으므로 스크립트에 직접 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-169">The application ID and tenant ID are not sensitive, so you can embed them directly in your script.</span></span> <span data-ttu-id="ebba9-170">테넌트 ID를 검색해야 할 경우 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-170">If you need to retrieve the tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

<span data-ttu-id="ebba9-171">응용 프로그램 ID를 검색해야 할 경우 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-171">If you need to retrieve the application ID, use:</span></span>

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="create-service-principal-with-certificate-from-certificate-authority"></a><span data-ttu-id="ebba9-172">인증 기관의 인증서를 사용하여 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="ebba9-172">Create service principal with certificate from Certificate Authority</span></span>
<span data-ttu-id="ebba9-173">인증 기관에서 발급한 인증서를 사용해서 서비스 주체를 만들려면 다음 스크립트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-173">To use a certificate issued from a Certificate Authority to create service principal, use the following script:</span></span>

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
    # Sleep here for a few seconds to allow the service principal application to become active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
 
 $NewRole
```

<span data-ttu-id="ebba9-174">스크립트에 대해 다음 사항을 알아두세요.</span><span class="sxs-lookup"><span data-stu-id="ebba9-174">A few items to note about the script:</span></span>

* <span data-ttu-id="ebba9-175">해당 구독으로 액세스 범위가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-175">Access is scoped to the subscription.</span></span>
* <span data-ttu-id="ebba9-176">이 예제에서는 참가자 역할에 서비스 주체를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-176">In this example, you add the service principal to the Contributor role.</span></span> <span data-ttu-id="ebba9-177">다른 역할에 대해서는 [RBAC: 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebba9-177">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="ebba9-178">이 스크립트는 새 서비스 주체가 Azure Active Directory 전체에 전파될 시간을 허용하기 위해 15분간 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-178">The script sleeps for 15 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="ebba9-179">스크립트가 대기하는 시간이 충분히 길지 않으면 "PrincipalNotFound: 보안 주체 {id}이(가) 디렉터리에 없습니다."라는 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-179">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span></span>
* <span data-ttu-id="ebba9-180">서비스 주체에게 더 많은 구독 또는 리소스 그룹에 대한 액세스 권한을 부여해야 할 경우 다른 범위를 지정해서 `New-AzureRMRoleAssignment` cmdlet을 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-180">If you need to grant the service principal access to more subscriptions or resource groups, run the `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>

### <a name="provide-certificate-through-automated-powershell-script"></a><span data-ttu-id="ebba9-181">자동화된 PowerShell 스크립트를 통해 인증서 제공</span><span class="sxs-lookup"><span data-stu-id="ebba9-181">Provide certificate through automated PowerShell script</span></span>
<span data-ttu-id="ebba9-182">서비스 주체로 로그인할 때마다 AD 앱에 디렉터리의 테넌트 ID를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-182">Whenever you sign in as a service principal, you need to provide the tenant id of the directory for your AD app.</span></span> <span data-ttu-id="ebba9-183">테넌트는 Azure Active Directory의 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-183">A tenant is an instance of Azure Active Directory.</span></span>

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

<span data-ttu-id="ebba9-184">응용 프로그램 ID 및 테넌트 ID는 대/소문자를 구분하지 않으므로 스크립트에 직접 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-184">The application ID and tenant ID are not sensitive, so you can embed them directly in your script.</span></span> <span data-ttu-id="ebba9-185">테넌트 ID를 검색해야 할 경우 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-185">If you need to retrieve the tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

<span data-ttu-id="ebba9-186">응용 프로그램 ID를 검색해야 할 경우 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-186">If you need to retrieve the application ID, use:</span></span>

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="change-credentials"></a><span data-ttu-id="ebba9-187">자격 증명 변경</span><span class="sxs-lookup"><span data-stu-id="ebba9-187">Change credentials</span></span>

<span data-ttu-id="ebba9-188">보안 위협 또는 자격 증명 만료 때문에 AD 앱에 대한 자격 증명을 변경하려면 [Remove-AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) 및 [New-AzureRmADAppCredential](/powershell/module/azurerm.resources/new-azurermadappcredential) cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-188">To change the credentials for an AD app, either because of a security compromise or a credential expiration, use the [Remove-AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) and [New-AzureRmADAppCredential](/powershell/module/azurerm.resources/new-azurermadappcredential) cmdlets.</span></span>

<span data-ttu-id="ebba9-189">응용 프로그램에 대한 자격 증명을 모두 제거하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-189">To remove all the credentials for an application, use:</span></span>

```powershell
Remove-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -All
```

<span data-ttu-id="ebba9-190">암호를 추가하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-190">To add a password, use:</span></span>

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -Password p@ssword!
```

<span data-ttu-id="ebba9-191">인증서 값을 추가하려면 이 항목에 설명된 대로 자체 서명된 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-191">To add a certificate value, create a self-signed certificate as shown in this topic.</span></span> <span data-ttu-id="ebba9-192">그 후 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-192">Then, use:</span></span>

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
```

## <a name="save-access-token-to-simplify-log-in"></a><span data-ttu-id="ebba9-193">액세스 토큰을 저장하여 로그인 단순화</span><span class="sxs-lookup"><span data-stu-id="ebba9-193">Save access token to simplify log in</span></span>
<span data-ttu-id="ebba9-194">로그인해야 할 때마다 서비스 주체 자격 증명을 제공하는 것을 피하기 위해 액세스 토큰을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-194">To avoid providing the service principal credentials every time it needs to log in, you can save the access token.</span></span>

<span data-ttu-id="ebba9-195">이후 세션에서 현재 액세스 토큰을 사용하기 위해 프로필을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-195">To use the current access token in a later session, save the profile.</span></span>
   
```powershell
Save-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```
   
<span data-ttu-id="ebba9-196">프로필을 열고 해당 내용을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-196">Open the profile and examine its contents.</span></span> <span data-ttu-id="ebba9-197">액세스 토큰을 포함하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-197">Notice that it contains an access token.</span></span> <span data-ttu-id="ebba9-198">수동으로 다시 로그인하는 대신 프로필을 로드하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-198">Instead of manually logging in again, simply load the profile.</span></span>
   
```powershell
Select-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```

> [!NOTE]
> <span data-ttu-id="ebba9-199">토큰이 유효한 한 저장된 프로필을 사용해야만 작동하므로 액세스 토큰이 만료됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-199">The access token expires, so using a saved profile only works for as long as the token is valid.</span></span>
>  

<span data-ttu-id="ebba9-200">또는 PowerShell에서 REST 작업을 호출하여 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-200">Alternatively, you can invoke REST operations from PowerShell to log in.</span></span> <span data-ttu-id="ebba9-201">인증 응답에서 다른 작업에 사용할 액세스 토큰을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-201">From the authentication response, you can retrieve the access token for use with other operations.</span></span> <span data-ttu-id="ebba9-202">REST 작업을 호출하여 액세스 토큰을 검색하는 예제는 [액세스 토큰 생성하기](resource-manager-rest-api.md#generating-an-access-token)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebba9-202">For an example of retrieving the access token by invoking REST operations, see [Generating an Access Token](resource-manager-rest-api.md#generating-an-access-token).</span></span>

## <a name="debug"></a><span data-ttu-id="ebba9-203">디버그</span><span class="sxs-lookup"><span data-stu-id="ebba9-203">Debug</span></span>

<span data-ttu-id="ebba9-204">서비스 주체를 만들 때 다음과 같은 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-204">You may encounter the following errors when creating a service principal:</span></span>

* <span data-ttu-id="ebba9-205">**"Authentication_Unauthorized"** 또는 **"컨텍스트에서 구독을 찾을 수 없습니다."**</span><span class="sxs-lookup"><span data-stu-id="ebba9-205">**"Authentication_Unauthorized"** or **"No subscription found in the context."**</span></span> <span data-ttu-id="ebba9-206">- 계정에 Azure Active Directory에서 앱을 등록하는 데 [필요한 권한](#required-permissions)이 없으면 이 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-206">- You see this error when your account does not have the [required permissions](#required-permissions) on the Azure Active Directory to register an app.</span></span> <span data-ttu-id="ebba9-207">일반적으로 Azure Active Directory의 관리 사용자만 앱을 등록할 수 있고 사용자 계정은 관리자가 아니면 이 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-207">Typically, you see this error when only admin users in your Azure Active Directory can register apps, and your account is not an admin.</span></span> <span data-ttu-id="ebba9-208">관리자 역할에 사용자를 할당하거나 사용자가 앱을 등록할 수 있게 설정하도록 관리자에게 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-208">Ask your administrator to either assign you to an administrator role, or to enable users to register apps.</span></span>

* <span data-ttu-id="ebba9-209">계정에 **"'/subscriptions/{guid}' 범위에 대해 'Microsoft.Authorization/roleAssignments/write' 작업을 수행할 수 있는 권한이 없습니다."** - 계정에 ID에 역할을 할당할 수 있는 충분한 권한이 없을 때 이 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-209">Your account **"does not have authorization to perform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/{guid}'."** - You see this error when your account does not have sufficient permissions to assign a role to an identity.</span></span> <span data-ttu-id="ebba9-210">구독 관리자에게 사용자 액세스 관리자 역할에 사용자를 추가할 것을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="ebba9-210">Ask your subscription administrator to add you to User Access Administrator role.</span></span>

## <a name="sample-applications"></a><span data-ttu-id="ebba9-211">샘플 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="ebba9-211">Sample applications</span></span>
<span data-ttu-id="ebba9-212">다른 플랫폼을 통해 응용 프로그램으로 로그인하는 방법에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebba9-212">For information about logging in as the application through different platforms, see:</span></span>

* [<span data-ttu-id="ebba9-213">.NET</span><span class="sxs-lookup"><span data-stu-id="ebba9-213">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="ebba9-214">Java</span><span class="sxs-lookup"><span data-stu-id="ebba9-214">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="ebba9-215">Node.JS</span><span class="sxs-lookup"><span data-stu-id="ebba9-215">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="ebba9-216">Python</span><span class="sxs-lookup"><span data-stu-id="ebba9-216">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="ebba9-217">Ruby</span><span class="sxs-lookup"><span data-stu-id="ebba9-217">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a><span data-ttu-id="ebba9-218">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ebba9-218">Next steps</span></span>
* <span data-ttu-id="ebba9-219">리소스 관리를 위해 Azure에 응용 프로그램을 통합하는 자세한 단계를 보려면 [Azure Resource Manager API를 사용한 권한 부여 개발자 가이드](resource-manager-api-authentication.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebba9-219">For detailed steps on integrating an application into Azure for managing resources, see [Developer's guide to authorization with the Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="ebba9-220">응용 프로그램 및 서비스 주체에 대한 자세한 내용은 [응용 프로그램 개체 및 서비스 주체 개체](../active-directory/active-directory-application-objects.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebba9-220">For a more detailed explanation of applications and service principals, see [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span> 
* <span data-ttu-id="ebba9-221">Azure Active Directory 인증에 대한 자세한 내용은 [Azure AD의 인증 시나리오](../active-directory/active-directory-authentication-scenarios.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebba9-221">For more information about Azure Active Directory authentication, see [Authentication Scenarios for Azure AD](../active-directory/active-directory-authentication-scenarios.md).</span></span>
* <span data-ttu-id="ebba9-222">권한이 부여되거나 사용자에 대해 거부될 수 있는 작업 목록은 [Azure Resource Manager 리소스 공급자 작업](../active-directory/role-based-access-control-resource-provider-operations.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebba9-222">For a list of available actions that can be granted or denied to users, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>

