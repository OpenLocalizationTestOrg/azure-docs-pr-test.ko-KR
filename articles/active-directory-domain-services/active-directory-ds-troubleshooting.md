---
title: "Azure Active Directory Domain Services: 문제 해결 가이드 | Microsoft Docs"
description: "Azure AD 도메인 서비스에 대한 문제 해결 가이드"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 4bc8c604-f57c-4f28-9dac-8b9164a0cf0b
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: d6695b0c40f56093e8701dfe6394143268114453
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad-domain-services---troubleshooting-guide"></a><span data-ttu-id="d7d90-103">Azure AD Domain Services - 문제 해결 가이드</span><span class="sxs-lookup"><span data-stu-id="d7d90-103">Azure AD Domain Services - Troubleshooting guide</span></span>
<span data-ttu-id="d7d90-104">이 문서는 Azure AD(Active Directory) 도메인 서비스를 설치하거나 관리할 때 발생할 수 있는 문제에 대한 문제 해결 힌트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-104">This article provides troubleshooting hints for issues you may encounter when setting up or administering Azure Active Directory (AD) Domain Services.</span></span>

## <a name="you-cannot-enable-azure-ad-domain-services-for-your-azure-ad-directory"></a><span data-ttu-id="d7d90-105">Azure AD 디렉터리에 대해 Azure AD Domain Services를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-105">You cannot enable Azure AD Domain Services for your Azure AD directory</span></span>
<span data-ttu-id="d7d90-106">이 섹션에서는 디렉터리에 대해 Azure AD Domain Services를 사용하도록 설정할 때 발생한 오류를 해결하는 데 도움이 되며 실패하거나 [사용 안 함]으로 다시 전환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-106">This section helps you troubleshoot errors when you try to enable Azure AD Domain Services for your directory and it fails or gets toggled back to 'Disabled'.</span></span>

<span data-ttu-id="d7d90-107">발생하는 오류 메시지에 해당하는 문제 해결 단계를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-107">Pick the troubleshooting steps that correspond to the error message you encounter.</span></span>

| <span data-ttu-id="d7d90-108">**오류 메시지**</span><span class="sxs-lookup"><span data-stu-id="d7d90-108">**Error Message**</span></span> | <span data-ttu-id="d7d90-109">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="d7d90-109">**Resolution**</span></span> |
| --- |:--- |
| <span data-ttu-id="d7d90-110">*contoso100.com 이름은 이 네트워크에서 이미 사용 중입니다. 사용하지 않는 이름을 지정하십시오.*</span><span class="sxs-lookup"><span data-stu-id="d7d90-110">*The name contoso100.com is already in use on this network. Specify a name that is not in use.*</span></span> |[<span data-ttu-id="d7d90-111">가상 네트워크에서 도메인 이름 충돌</span><span class="sxs-lookup"><span data-stu-id="d7d90-111">Domain name conflict in the virtual network</span></span>](active-directory-ds-troubleshooting.md#domain-name-conflict) |
| <span data-ttu-id="d7d90-112">*이 Azure AD 테넌트에서는 Domain Services를 사용할 수 없습니다. 이 서비스에는 'Azure AD Domain Services Sync'라는 응용 프로그램에 대한 적절한 권한이 없습니다. 'Azure AD Domain Services Sync'라는 응용 프로그램을 삭제한 다음 Azure AD 테넌트에 대해 Domain Services를 사용하도록 설정하십시오.*</span><span class="sxs-lookup"><span data-stu-id="d7d90-112">*Domain Services could not be enabled in this Azure AD tenant. The service does not have adequate permissions to the application called 'Azure AD Domain Services Sync'. Delete the application called 'Azure AD Domain Services Sync' and then try to enable Domain Services for your Azure AD tenant.*</span></span> |[<span data-ttu-id="d7d90-113">Domain Services에 Azure AD Domain Services Sync 응용 프로그램에 대한 적절한 권한이 없음</span><span class="sxs-lookup"><span data-stu-id="d7d90-113">Domain Services does not have adequate permissions to the Azure AD Domain Services Sync application</span></span>](active-directory-ds-troubleshooting.md#inadequate-permissions) |
| <span data-ttu-id="d7d90-114">*이 Azure AD 테넌트에서는 Domain Services를 사용할 수 없습니다. Azure AD 테넌트의 Domain Services 응용 프로그램에는 Domain Services를 사용하는 데 필요한 권한이 없습니다. d87dcbc6-a371-462e-88e3-28ad15ec4e64 응용 프로그램 식별자를 사용하여 응용 프로그램을 삭제한 다음 Azure AD 테넌트에 대해 Domain Services를 사용하도록 설정하십시오.*</span><span class="sxs-lookup"><span data-stu-id="d7d90-114">*Domain Services could not be enabled in this Azure AD tenant. The Domain Services application in your Azure AD tenant does not have the required permissions to enable Domain Services. Delete the application with the application identifier d87dcbc6-a371-462e-88e3-28ad15ec4e64 and then try to enable Domain Services for your Azure AD tenant.*</span></span> |[<span data-ttu-id="d7d90-115">테넌트에서 Domain Services 응용 프로그램을 제대로 구성하지 않음</span><span class="sxs-lookup"><span data-stu-id="d7d90-115">The Domain Services application is not configured properly in your tenant</span></span>](active-directory-ds-troubleshooting.md#invalid-configuration) |
| <span data-ttu-id="d7d90-116">*이 Azure AD 테넌트에서는 Domain Services를 사용할 수 없습니다. Azure AD 테넌트에서 Microsoft Azure AD 응용 프로그램을 사용할 수 없습니다. 00000002-0000-0000-c000-000000000000 응용 프로그램 식별자를 사용하여 응용 프로그램을 사용하도록 설정한 다음 Azure AD 테넌트에 대해 Domain Services를 사용하도록 설정하십시오.*</span><span class="sxs-lookup"><span data-stu-id="d7d90-116">*Domain Services could not be enabled in this Azure AD tenant. The Microsoft Azure AD application is disabled in your Azure AD tenant. Enable the application with the application identifier 00000002-0000-0000-c000-000000000000 and then try to enable Domain Services for your Azure AD tenant.*</span></span> |[<span data-ttu-id="d7d90-117">Azure AD 테넌트에서 Microsoft Graph 응용 프로그램을 사용할 수 없음</span><span class="sxs-lookup"><span data-stu-id="d7d90-117">The Microsoft Graph application is disabled in your Azure AD tenant</span></span>](active-directory-ds-troubleshooting.md#microsoft-graph-disabled) |

### <a name="domain-name-conflict"></a><span data-ttu-id="d7d90-118">도메인 이름 충돌</span><span class="sxs-lookup"><span data-stu-id="d7d90-118">Domain Name conflict</span></span>
<span data-ttu-id="d7d90-119">**오류 메시지:**</span><span class="sxs-lookup"><span data-stu-id="d7d90-119">**Error message:**</span></span>

<span data-ttu-id="d7d90-120">*contoso100.com 이름은 이 네트워크에서 이미 사용 중입니다. 사용하지 않는 이름을 지정하십시오.*</span><span class="sxs-lookup"><span data-stu-id="d7d90-120">*The name contoso100.com is already in use on this network. Specify a name that is not in use.*</span></span>

<span data-ttu-id="d7d90-121">**재구성:**</span><span class="sxs-lookup"><span data-stu-id="d7d90-121">**Remediation:**</span></span>

<span data-ttu-id="d7d90-122">해당 가상 네트워크에서 동일한 도메인 이름을 사용하는 기존 도메인이 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-122">Ensure that you do not have an existing domain with the same domain name available on that virtual network.</span></span> <span data-ttu-id="d7d90-123">예를 들어, 선택한 가상 네트워크에서 'contoso.com'이라는 도메인을 이미 사용한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-123">For instance, assume you have a domain called 'contoso.com' already available on the selected virtual network.</span></span> <span data-ttu-id="d7d90-124">나중에 해당 가상 네트워크에서 동일한 도메인 이름(즉, 'contoso.com')을 가진 Azure AD Domain Services 관리되는 도메인을 사용하도록 설정하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-124">Later, you try to enable an Azure AD Domain Services managed domain with the same domain name (that is, 'contoso.com') on that virtual network.</span></span> <span data-ttu-id="d7d90-125">Azure AD 도메인 서비스를 사용하도록 설정하면 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-125">You encounter a failure when trying to enable Azure AD Domain Services.</span></span>

<span data-ttu-id="d7d90-126">이 오류는 해당 가상 네트워크에서 도메인 이름이 충돌하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-126">This failure is due to name conflicts for the domain name on that virtual network.</span></span> <span data-ttu-id="d7d90-127">이 경우 다른 이름을 사용하여 Azure AD 도메인 서비스 관리되는 도메인을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-127">In this situation, you must use a different name to set up your Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="d7d90-128">또는 기존 도메인을 프로비전 해제한 후 Azure AD 도메인 서비스를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-128">Alternately, you can de-provision the existing domain and then proceed to enable Azure AD Domain Services.</span></span>

### <a name="inadequate-permissions"></a><span data-ttu-id="d7d90-129">부적절한 권한</span><span class="sxs-lookup"><span data-stu-id="d7d90-129">Inadequate permissions</span></span>
<span data-ttu-id="d7d90-130">**오류 메시지:**</span><span class="sxs-lookup"><span data-stu-id="d7d90-130">**Error message:**</span></span>

<span data-ttu-id="d7d90-131">*이 Azure AD 테넌트에서는 Domain Services를 사용할 수 없습니다. 이 서비스에는 'Azure AD Domain Services Sync'라는 응용 프로그램에 대한 적절한 권한이 없습니다. 'Azure AD Domain Services Sync'라는 응용 프로그램을 삭제한 다음 Azure AD 테넌트에 대해 Domain Services를 사용하도록 설정하십시오.*</span><span class="sxs-lookup"><span data-stu-id="d7d90-131">*Domain Services could not be enabled in this Azure AD tenant. The service does not have adequate permissions to the application called 'Azure AD Domain Services Sync'. Delete the application called 'Azure AD Domain Services Sync' and then try to enable Domain Services for your Azure AD tenant.*</span></span>

<span data-ttu-id="d7d90-132">**재구성:**</span><span class="sxs-lookup"><span data-stu-id="d7d90-132">**Remediation:**</span></span>

<span data-ttu-id="d7d90-133">Azure AD 디렉터리에 'Azure AD Domain Services Sync'라는 이름의 응용 프로그램이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-133">Check to see if there is an application with the name 'Azure AD Domain Services Sync' in your Azure AD directory.</span></span> <span data-ttu-id="d7d90-134">이 응용 프로그램이 있으면 삭제한 다음 Azure AD Domain Services를 사용하도록 다시 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-134">If this application exists, delete it and then re-enable Azure AD Domain Services.</span></span>

<span data-ttu-id="d7d90-135">다음 단계를 수행하여 응용 프로그램이 있는지 확인하고 있는 경우 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-135">Perform the following steps to check for the presence of the application and to delete it, if the application exists:</span></span>

1. <span data-ttu-id="d7d90-136">**Azure 클래식 포털** ([https://manage.windowsazure.com](https://manage.windowsazure.com))로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-136">Navigate to the **Azure classic portal** ([https://manage.windowsazure.com](https://manage.windowsazure.com)).</span></span>
2. <span data-ttu-id="d7d90-137">왼쪽 창에서 **Active Directory** 노드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-137">Select the **Active Directory** node on the left pane.</span></span>
3. <span data-ttu-id="d7d90-138">Azure AD 도메인 서비스를 사용하도록 설정할 Azure AD 테넌트(디렉터리)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-138">Select the Azure AD tenant (directory) for which you would like to enable Azure AD Domain Services.</span></span>
4. <span data-ttu-id="d7d90-139">**응용 프로그램** 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-139">Navigate to the **Applications** tab.</span></span>
5. <span data-ttu-id="d7d90-140">드롭다운에서 **회사가 보유한 응용 프로그램** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-140">Select the **Applications my company owns** option in the dropdown.</span></span>
6. <span data-ttu-id="d7d90-141">**Azure AD Domain Services 동기화**라는 응용 프로그램이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-141">Check for an application called **Azure AD Domain Services Sync**.</span></span> <span data-ttu-id="d7d90-142">응용 프로그램이 있는 경우 삭제를 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-142">If the application exists, proceed to delete it.</span></span>
7. <span data-ttu-id="d7d90-143">응용 프로그램을 삭제한 후에는 Azure AD 도메인 서비스를 다시 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-143">Once you have deleted the application, try to enable Azure AD Domain Services once again.</span></span>

### <a name="invalid-configuration"></a><span data-ttu-id="d7d90-144">유효하지 않은 구성</span><span class="sxs-lookup"><span data-stu-id="d7d90-144">Invalid configuration</span></span>
<span data-ttu-id="d7d90-145">**오류 메시지:**</span><span class="sxs-lookup"><span data-stu-id="d7d90-145">**Error message:**</span></span>

<span data-ttu-id="d7d90-146">*이 Azure AD 테넌트에서는 Domain Services를 사용할 수 없습니다. Azure AD 테넌트의 Domain Services 응용 프로그램에는 Domain Services를 사용하는 데 필요한 권한이 없습니다. d87dcbc6-a371-462e-88e3-28ad15ec4e64 응용 프로그램 식별자를 사용하여 응용 프로그램을 삭제한 다음 Azure AD 테넌트에 대해 Domain Services를 사용하도록 설정하십시오.*</span><span class="sxs-lookup"><span data-stu-id="d7d90-146">*Domain Services could not be enabled in this Azure AD tenant. The Domain Services application in your Azure AD tenant does not have the required permissions to enable Domain Services. Delete the application with the application identifier d87dcbc6-a371-462e-88e3-28ad15ec4e64 and then try to enable Domain Services for your Azure AD tenant.*</span></span>

<span data-ttu-id="d7d90-147">**재구성:**</span><span class="sxs-lookup"><span data-stu-id="d7d90-147">**Remediation:**</span></span>

<span data-ttu-id="d7d90-148">Azure AD 디렉터리에 'AzureActiveDirectoryDomainControllerServices'(응용 프로그램 식별자가 d87dcbc6-a371-462e-88e3-28ad15ec4e64임)라는 이름의 응용 프로그램이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-148">Check to see if you have an application with the name 'AzureActiveDirectoryDomainControllerServices' (with an application identifier of d87dcbc6-a371-462e-88e3-28ad15ec4e64) in your Azure AD directory.</span></span> <span data-ttu-id="d7d90-149">이 응용 프로그램이 있는 경우 삭제한 다음 Azure AD Domain Services를 다시 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-149">If this application exists, you need to delete it and then re-enable Azure AD Domain Services.</span></span>

<span data-ttu-id="d7d90-150">다음 PowerShell 스크립트를 사용하여 응용 프로그램을 찾아 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-150">Use the following PowerShell script to find the application and delete it.</span></span>

> [!NOTE]
> <span data-ttu-id="d7d90-151">이 스크립트는 **Azure AD PowerShell 버전 2** cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-151">This script uses **Azure AD PowerShell version 2** cmdlets.</span></span> <span data-ttu-id="d7d90-152">사용 가능한 모든 cmdlet의 전체 목록을 보고 모듈을 다운로드하려면 [AzureAD PowerShell 참조 설명서](https://msdn.microsoft.com/library/azure/mt757189.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d7d90-152">For a full list of all available cmdlets and to download the module, read the [AzureAD PowerShell reference documentation](https://msdn.microsoft.com/library/azure/mt757189.aspx).</span></span>
>
>

```
$InformationPreference = "Continue"
$WarningPreference = "Continue"

$aadDsSp = Get-AzureADServicePrincipal -Filter "AppId eq 'd87dcbc6-a371-462e-88e3-28ad15ec4e64'" -ErrorAction Ignore
if ($aadDsSp -ne $null)
{
    Write-Information "Found Azure AD Domain Services application. Deleting it ..."
    Remove-AzureADServicePrincipal -ObjectId $aadDsSp.ObjectId
    Write-Information "Deleted the Azure AD Domain Services application."
}

$identifierUri = "https://sync.aaddc.activedirectory.windowsazure.com"
$appFilter = "IdentifierUris eq '" + $identifierUri + "'"
$app = Get-AzureADApplication -Filter $appFilter
if ($app -ne $null)
{
    Write-Information "Found Azure AD Domain Services Sync application. Deleting it ..."
    Remove-AzureADApplication -ObjectId $app.ObjectId
    Write-Information "Deleted the Azure AD Domain Services Sync application."
}

$spFilter = "ServicePrincipalNames eq '" + $identifierUri + "'"
$sp = Get-AzureADServicePrincipal -Filter $spFilter
if ($sp -ne $null)
{
    Write-Information "Found Azure AD Domain Services Sync service principal. Deleting it ..."
    Remove-AzureADServicePrincipal -ObjectId $sp.ObjectId
    Write-Information "Deleted the Azure AD Domain Services Sync service principal."
}
```
<br>

### <a name="microsoft-graph-disabled"></a><span data-ttu-id="d7d90-153">Microsoft Graph 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="d7d90-153">Microsoft Graph disabled</span></span>
<span data-ttu-id="d7d90-154">**오류 메시지:**</span><span class="sxs-lookup"><span data-stu-id="d7d90-154">**Error message:**</span></span>

<span data-ttu-id="d7d90-155">이 Azure AD 테넌트에서는 Domain Services를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-155">Domain Services could not be enabled in this Azure AD tenant.</span></span> <span data-ttu-id="d7d90-156">Azure AD 테넌트에서 Microsoft Azure AD 응용 프로그램을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-156">The Microsoft Azure AD application is disabled in your Azure AD tenant.</span></span> <span data-ttu-id="d7d90-157">00000002-0000-0000-c000-000000000000 응용 프로그램 식별자를 사용하여 응용 프로그램을 사용하도록 설정한 다음 Azure AD 테넌트에 대해 Domain Services를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-157">Enable the application with the application identifier 00000002-0000-0000-c000-000000000000 and then try to enable Domain Services for your Azure AD tenant.</span></span>

<span data-ttu-id="d7d90-158">**재구성:**</span><span class="sxs-lookup"><span data-stu-id="d7d90-158">**Remediation:**</span></span>

<span data-ttu-id="d7d90-159">00000002-0000-0000-c000-000000000000 식별자를 사용하는 응용 프로그램을 사용하지 않도록 설정했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-159">Check to see if you have disabled an application with the identifier 00000002-0000-0000-c000-000000000000.</span></span> <span data-ttu-id="d7d90-160">이 응용 프로그램은 Microsoft Azure AD 응용 프로그램이며 Azure AD 테넌트에 Graph API 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-160">This application is the Microsoft Azure AD application and provides Graph API access to your Azure AD tenant.</span></span> <span data-ttu-id="d7d90-161">Azure AD Domain Services는 이 응용 프로그램을 사용하여 Azure AD 테넌트와 관리되는 도메인을 동기화 할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-161">Azure AD Domain Services needs this application to be enabled to synchronize your Azure AD tenant to your managed domain.</span></span>

<span data-ttu-id="d7d90-162">이 오류를 해결하려면 이 응용 프로그램을 사용하도록 설정한 다음 Azure AD 테넌트에 대해 Domain Services를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-162">To resolve this error, enable this application and then try to enable Domain Services for your Azure AD tenant.</span></span>

## <a name="users-are-unable-to-sign-in-to-the-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="d7d90-163">사용자는 Azure AD 도메인 서비스 관리된 도메인에 로그인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-163">Users are unable to sign in to the Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="d7d90-164">Azure AD 테넌트에서 하나 이상의 사용자가 새로 만든 관리되는 도메인에 로그인할 수 없는 경우 다음 문제 해결 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-164">If one or more users in your Azure AD tenant are unable to sign in to the newly created managed domain, perform the following troubleshooting steps:</span></span>

* <span data-ttu-id="d7d90-165">**UPN 형식을 사용한 로그인:** SAMAccountName 형식('CONTOSO \ joeuser') 대신 UPN 형식(예: 'joeuser@contoso.com')을 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-165">**Sign-in using UPN format:** Try to sign in using the UPN format (for example, 'joeuser@contoso.com') instead of the SAMAccountName format ('CONTOSO\joeuser').</span></span> <span data-ttu-id="d7d90-166">UPN 접두사가 너무 길거나 관리되는 도메인의 다른 사용자와 동일한 사용자에 대해 SAMAccountName이 자동으로 생성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-166">The SAMAccountName may be automatically generated for users whose UPN prefix is overly long or is the same as another user on the managed domain.</span></span> <span data-ttu-id="d7d90-167">UPN 형식은 Azure AD 테넌트 내에서 고유하도록 보장됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-167">The UPN format is guaranteed to be unique within an Azure AD tenant.</span></span>

> [!NOTE]
> <span data-ttu-id="d7d90-168">Azure AD Domain Services 관리되는 도메인에 로그인하는 데 UPN 형식을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-168">We recommend using the UPN format to sign in to the Azure AD Domain Services managed domain.</span></span>
>
>

* <span data-ttu-id="d7d90-169">시작 가이드에 설명된 단계에 따라 [암호 동기화를 사용하도록 설정](active-directory-ds-getting-started-password-sync.md) 했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-169">Ensure that you have [enabled password synchronization](active-directory-ds-getting-started-password-sync.md) in accordance with the steps outlined in the Getting Started guide.</span></span>
* <span data-ttu-id="d7d90-170">**외부 계정:** 영향을 받는 사용자 계정이 Azure AD 테넌트에서 외부 계정이 아닌지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-170">**External accounts:** Ensure that the affected user account is not an external account in the Azure AD tenant.</span></span> <span data-ttu-id="d7d90-171">외부 계정의 예는 Microsoft 계정(예: 'joe@live.com') 또는 외부 Azure AD 디렉터리에서 사용자 계정을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-171">Examples of external accounts include Microsoft accounts (for example, 'joe@live.com') or user accounts from an external Azure AD directory.</span></span> <span data-ttu-id="d7d90-172">Azure AD 도메인 서비스에는 이러한 사용자 계정에 대한 자격 증명이 없으므로 이러한 사용자는 관리된 도메인에 로그인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-172">Since Azure AD Domain Services does not have credentials for such user accounts, these users cannot sign in to the managed domain.</span></span>
* <span data-ttu-id="d7d90-173">**동기화된 계정:** 영향을 받는 사용자 계정이 온-프레미스 디렉터리에서 동기화되는 경우 다음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-173">**Synced accounts:** If the affected user accounts are synchronized from an on-premises directory, verify that:</span></span>

  * <span data-ttu-id="d7d90-174">[Azure AD Connect의 최신 권장 사항](https://www.microsoft.com/en-us/download/details.aspx?id=47594)으로 배포하거나 업데이트했습니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-174">You have deployed or updated to the [latest recommended release of Azure AD Connect](https://www.microsoft.com/en-us/download/details.aspx?id=47594).</span></span>
  * <span data-ttu-id="d7d90-175">[전체 동기화를 수행](active-directory-ds-getting-started-password-sync.md)하도록 Azure AD Connect를 구성했습니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-175">You have configured Azure AD Connect to [perform a full synchronization](active-directory-ds-getting-started-password-sync.md).</span></span>
  * <span data-ttu-id="d7d90-176">디렉터리의 크기에 따라 사용자 계정 및 해시 자격 증명이 Azure AD 도메인 서비스에서 사용할 수 있도록 하는 데 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-176">Depending on the size of your directory, it may take a while for user accounts and credential hashes to be available in Azure AD Domain Services.</span></span> <span data-ttu-id="d7d90-177">인증을 다시 시도하기 전에 충분한 시간 동안 대기합니다(디렉터리 크기에 따라 몇 시간에서 큰 디렉터리는 하루나 이틀까지).</span><span class="sxs-lookup"><span data-stu-id="d7d90-177">Ensure you wait long enough before retrying authentication (depending on the size of your directory - a few hours to a day or two for large directories).</span></span>
  * <span data-ttu-id="d7d90-178">앞의 단계를 확인한 후에도 문제가 지속되면 Microsoft Azure AD Sync 서비스를 다시 시작해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-178">If the issue persists after verifying the preceding steps, try restarting the Microsoft Azure AD Sync Service.</span></span> <span data-ttu-id="d7d90-179">동기화 컴퓨터에서 명령 프롬프트를 시작하고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-179">From your sync machine, launch a command prompt and execute the following commands:</span></span>

    1. <span data-ttu-id="d7d90-180">net stop 'Microsoft Azure AD Sync'</span><span class="sxs-lookup"><span data-stu-id="d7d90-180">net stop 'Microsoft Azure AD Sync'</span></span>
    2. <span data-ttu-id="d7d90-181">net start 'Microsoft Azure AD Sync'</span><span class="sxs-lookup"><span data-stu-id="d7d90-181">net start 'Microsoft Azure AD Sync'</span></span>
* <span data-ttu-id="d7d90-182">**클라우드 전용 계정**: 영향을 받는 사용자 계정이 클라우드 전용 사용자 계정인 경우 사용자는 Azure AD 도메인 서비스를 사용하도록 설정한 후에 자신의 암호를 변경하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-182">**Cloud-only accounts**: If the affected user account is a cloud-only user account, ensure that the user has changed their password after you enabled Azure AD Domain Services.</span></span> <span data-ttu-id="d7d90-183">이 단계를 수행하면 Azure AD 도메인 서비스가 생성되는 데 필요한 자격 증명 해시가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-183">This step causes the credential hashes required for Azure AD Domain Services to be generated.</span></span>

## <a name="users-removed-from-your-azure-ad-tenant-are-not-removed-from-your-managed-domain"></a><span data-ttu-id="d7d90-184">Azure AD 테넌트에서는 제거되지만 관리되는 도메인에서는 제거되지 않는 사용자</span><span class="sxs-lookup"><span data-stu-id="d7d90-184">Users removed from your Azure AD tenant are not removed from your managed domain</span></span>
<span data-ttu-id="d7d90-185">Azure AD에서는 사용자 개체를 실수로 삭제하지 못하도록 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-185">Azure AD protects you from accidental deletion of user objects.</span></span> <span data-ttu-id="d7d90-186">Azure AD 테넌트에서 사용자 계정을 삭제하면 해당 사용자 개체가 휴지통으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-186">When you delete a user account from your Azure AD tenant, the corresponding user object is moved to the Recycle Bin.</span></span> <span data-ttu-id="d7d90-187">이 삭제 작업이 관리되는 도메인과 동기화하면 해당 사용자 계정을 사용할 수 없는 것으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-187">When this delete operation is synchronized to your managed domain, it causes the corresponding user account to be marked disabled.</span></span> <span data-ttu-id="d7d90-188">이 기능을 사용하면 나중에 사용자 계정을 복구하거나 삭제를 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-188">This feature helps you recover or undelete the user account later.</span></span>

<span data-ttu-id="d7d90-189">Azure AD 디렉터리에서 동일한 UPN을 사용하여 사용자 계정을 다시 만든 경우에도 사용자 계정은 관리되는 도메인에서 사용할 수 없는 상태로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-189">The user account remains in the disabled state in your managed domain, even if you re-create a user account with the same UPN in your Azure AD directory.</span></span> <span data-ttu-id="d7d90-190">관리되는 도메인에서 사용자 계정을 제거하려면 Azure AD 테넌트에서 사용자를 강제로 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-190">To remove the user account from your managed domain, you need to force delete it from your Azure AD tenant.</span></span>

<span data-ttu-id="d7d90-191">관리되는 도메인에서 사용자 계정을 완전히 제거하려면 Azure AD 테넌트에서 사용자를 영구적으로 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-191">To remove the user account fully from your managed domain, delete the user permanently from your Azure AD tenant.</span></span> <span data-ttu-id="d7d90-192">이 [MSDN 문서](https://msdn.microsoft.com/library/azure/dn194132.aspx)에서 설명한 대로 '-RemoveFromRecycleBin' 옵션을 포함한 Remove-MsolUser PowerShell cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d7d90-192">Use the Remove-MsolUser PowerShell cmdlet with the '-RemoveFromRecycleBin' option, as described in this [MSDN article](https://msdn.microsoft.com/library/azure/dn194132.aspx).</span></span>

## <a name="contact-us"></a><span data-ttu-id="d7d90-193">문의처</span><span class="sxs-lookup"><span data-stu-id="d7d90-193">Contact Us</span></span>
<span data-ttu-id="d7d90-194">[지원이 필요하거나 피드백을 공유하려면](active-directory-ds-contact-us.md)Azure Active Directory Domain Services 제품 팀에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="d7d90-194">Contact the Azure Active Directory Domain Services product team to [share feedback or for support](active-directory-ds-contact-us.md).</span></span>
